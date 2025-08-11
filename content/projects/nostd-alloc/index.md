---
title: "nostd-alloc: Custom Memory Allocator"
date: 2024-11-20T14:00:00-00:00
draft: false
description: "Custom memory allocation library for no_std Rust environments"
tags: ["rust", "memory-management", "systems-programming", "embedded", "no-std"]
categories: ["systems"]
---

## Overview

Custom memory allocator and basic collections implementation for `no_std` Rust environments. Built from first principles without standard library dependencies.

## Core Implementation

### Memory Allocator
```rust
use core::alloc::{GlobalAlloc, Layout};

pub struct CustomAllocator {
    heap_start: usize,
    heap_size: usize,
    free_list: *mut FreeBlock,
}

unsafe impl GlobalAlloc for CustomAllocator {
    unsafe fn alloc(&self, layout: Layout) -> *mut u8 {
        self.allocate_block(layout.size(), layout.align())
    }
    
    unsafe fn dealloc(&self, ptr: *mut u8, layout: Layout) {
        self.deallocate_block(ptr, layout.size())
    }
}
```

### Block Management
- **Free list algorithm**: Linked list of available memory blocks
- **Coalescing**: Merging adjacent free blocks to reduce fragmentation
- **Alignment handling**: Proper memory alignment for different data types
- **Metadata overhead**: Minimal header information per allocation

### Data Structures

#### Custom Vec Implementation
```rust
pub struct Vec<T> {
    ptr: *mut T,
    len: usize,
    cap: usize,
}

impl<T> Vec<T> {
    pub fn push(&mut self, item: T) -> Result<(), AllocError> {
        if self.len == self.cap {
            self.grow()?;
        }
        unsafe {
            ptr::write(self.ptr.add(self.len), item);
        }
        self.len += 1;
        Ok(())
    }
}
```

#### Custom String Implementation
```rust
pub struct String {
    vec: Vec<u8>,
}

impl String {
    pub fn push_str(&mut self, s: &str) -> Result<(), AllocError> {
        for byte in s.bytes() {
            self.vec.push(byte)?;
        }
        Ok(())
    }
}
```

## Memory Management Strategy

### Allocation Algorithm
- **First-fit**: Fast allocation with acceptable fragmentation
- **Boundary tags**: Header and footer for each block
- **Free block merging**: Automatic coalescing on deallocation

### Performance Characteristics
- **Allocation time**: O(n) worst-case for first-fit
- **Deallocation time**: O(1) with coalescing
- **Memory overhead**: 16 bytes per allocation for metadata
- **Fragmentation**: Mitigated through block coalescing

## System Integration

### mmap System Calls
```rust
fn allocate_heap(size: usize) -> Result<*mut u8, AllocError> {
    let ptr = unsafe {
        mmap(
            ptr::null_mut(),
            size,
            PROT_READ | PROT_WRITE,
            MAP_PRIVATE | MAP_ANONYMOUS,
            -1,
            0,
        )
    };
    
    if ptr == MAP_FAILED {
        return Err(AllocError::OutOfMemory);
    }
    
    Ok(ptr as *mut u8)
}
```

### Error Handling
- **Custom error types**: Structured error handling without std
- **Result-based APIs**: All fallible operations return Results
- **Panic-free operation**: No panics in core allocation paths

## Testing & Validation

### Unit Tests
- **Allocation/deallocation cycles**: Verify memory reclamation
- **Alignment verification**: Ensure proper pointer alignment
- **Fragmentation testing**: Stress test allocation patterns
- **Concurrent access**: Thread safety validation (where applicable)

### Memory Safety
- **Use-after-free prevention**: Poisoning freed memory in debug builds
- **Double-free detection**: Tracking allocation state
- **Buffer overflow protection**: Bounds checking in debug mode

## Embedded Compatibility

### Resource Constraints
- **Fixed heap size**: Pre-allocated memory pool
- **No dynamic growth**: Bounded memory usage
- **Minimal stack usage**: Iterative algorithms over recursive
- **Zero dependencies**: Pure `no_std` implementation

### Platform Support
- **ARM Cortex-M**: Embedded microcontroller support
- **RISC-V**: Support for RISC-V architectures
- **x86_64**: Development and testing platform

## Links
- 📁 [Source Code](https://github.com/jmccrystal/nostd-alloc)
- 🦀 [Rust no_std Documentation](https://docs.rust-embedded.org/book/intro/no-std.html)
- 📚 [The Rust Reference](https://doc.rust-lang.org/reference/)

---

*Low-level systems programming demonstrating memory management fundamentals and bare-metal Rust development.*