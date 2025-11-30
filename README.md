# tszig-runtime

Runtime support library for TSZig-generated Zig code.

## Overview

`tszig-runtime` provides helper functions and utilities used by Zig code generated from TSZig transpilation. This includes string operations, console output, memory management helpers, and more.

## Components

| Module | Description |
|--------|-------------|
| `strings.zig` | String concatenation, indexing, and manipulation |
| `console.zig` | `console.log()` implementation |
| `printf.zig` | C-style `printf()` implementation |
| `memory.zig` | Allocator wrappers and memory utilities |
| `defer.zig` | Auto-defer helpers for resource cleanup |

## Installation

### As a Zig Dependency

Add to your `build.zig.zon`:

```zon
.{
    .dependencies = .{
        .tszig_runtime = .{
            .url = "https://github.com/TSZig/tszig-runtime/archive/refs/tags/v0.1.0.tar.gz",
            .hash = "...",
        },
    },
}
```

## Usage

```zig
const runtime = @import("tszig-runtime");

pub fn main() void {
    // String operations
    const greeting = runtime.stringConcat("Hello, ", "World!");
    
    // Console output
    runtime.consoleLog("{s}\n", .{greeting});
    
    // Printf-style output
    runtime.printf("Value: %d\n", .{42});
}
```

## API Reference

### String Operations

```zig
/// Concatenate two strings
pub fn stringConcat(a: []const u8, b: []const u8) []const u8

/// Access character at index (returns as string)
pub fn indexAccess(str: []const u8, idx: usize) []const u8

/// Get string length as f64 (for TypeScript compatibility)
pub fn stringLength(str: []const u8) f64
```

### Console Output

```zig
/// console.log() implementation
pub fn consoleLog(comptime fmt: []const u8, args: anytype) void

/// C-style printf() implementation
pub fn printf(comptime fmt: []const u8, args: anytype) void
```

### Memory Utilities

```zig
/// Consume a value (prevents unused variable errors)
pub fn consume(value: anytype) void

/// Get default allocator
pub fn getDefaultAllocator() std.mem.Allocator
```

## Generated Code Example

TSZig generates code that uses this runtime:

```typescript
// TypeScript input
const message: string = "Hello" + " " + "World";
console.log(message);
```

```zig
// Generated Zig
const runtime = @import("tszig-runtime");

pub fn main() void {
    const message = runtime.stringConcat("Hello", runtime.stringConcat(" ", "World"));
    runtime.consoleLog("{s}\n", .{message});
}
```

## License

MIT License - see [LICENSE](LICENSE) for details.

## Contributing

See [CONTRIBUTING.md](https://github.com/TSZig/.github/blob/main/CONTRIBUTING.md) for guidelines.
