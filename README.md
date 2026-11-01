# sword-glfw

Idiomatic, low-overhead GLFW bindings for the Sword programming language. This library provides the foundation for window management, OpenGL context creation, and Vulkan surface querying by wrapping the C Foreign Function Interface (FFI).

## Dependencies
The library utilizes Sword's direct dynamic linking via `extern "glfw"`. You do not need to compile GLFW from source alongside your project. Simply ensure that the native GLFW dynamic library (e.g., `libglfw.so` on Linux, `glfw3.dll` on Windows, or the Homebrew equivalent on macOS) is available on your host system at runtime.

## Setup

**sword-glfw** is distributed as a standard Sword module (`github.com/dsaragoza/sword-glfw`) and can be added to any Sword project with a `sword.mod` file using `shield`.

**Step-by-step installation:**

1. **Initialize a Sword module** in your project directory (if you do not already have a `sword.mod` file):
   ```bash
   shield new example.com/my-app
   cd my-app
   ```
2. **Fetch and add `sword-glfw` to your `sword.mod`**:
   ```bash
   shield get github.com/dsaragoza/sword-glfw
   ```
3. **Import the package** in your `.sword` source files:
   ```sword
   import "github.com/dsaragoza/sword-glfw"
   ```
   The package is exposed under the `glfw` namespace (`glfw.Init()`, `glfw.CreateWindow()`, etc.).


## Quickstart
Below is a classic example of creating a window and running a main event loop with an active OpenGL context:

```sword
import "github.com/dsaragoza/sword-glfw"

func main() int {
    mut window glfw.Window = nil 
    if !glfw.Init() {
        return -1
    }

    window = glfw.CreateWindow(640, 480, "Hello, World!", nil, nil)
    if window == nil {
        glfw.Terminate()
        return -1
    }

    glfw.MakeContextCurrent(window)

    for {
        if glfw.WindowShouldClose(window) {
            break
        }

        glfw.SwapBuffers(window)
        glfw.PollEvents()
    }

    glfw.Terminate()
    return 0
}
```

Compile and run your project with:
```bash
shield . -o app
./app
```


## Implementation Status

| Category | C GLFW Function | Sword Equivalent | Status |
| :--- | :--- | :--- | :--- |
| **Window Lifecycle** | `glfwInit` | `glfw.Init()` | Implemented |
| | `glfwTerminate` | `glfw.Terminate()` | Implemented |
| | `glfwWindowHint` | `glfw.WindowHint()` | Implemented |
| | `glfwCreateWindow` | `glfw.CreateWindow()` | Implemented |
| | `glfwDestroyWindow` | `glfw.DestroyWindow()` | Implemented |
| | `glfwWindowShouldClose`| `glfw.WindowShouldClose()` | Implemented |
| | `glfwPollEvents` | `glfw.PollEvents()` | Implemented |
| **OpenGL Context** | `glfwMakeContextCurrent` | `glfw.MakeContextCurrent()` | Implemented |
| | `glfwSwapBuffers` | `glfw.SwapBuffers()` | Implemented |
| | `glfwGetProcAddress` | `glfw.GetProcAddress()` | Implemented |
| | `glfwGetFramebufferSize` | `glfw.GetFramebufferSize()` | Implemented |
| **Diagnostics** | `glfwGetVersionString` | `glfw.GetVersionString()` | Implemented |
| | `glfwGetError` | `glfw.GetError()` | Implemented |
| **Vulkan (Base)** | `glfwVulkanSupported` | `glfw.VulkanSupported()` | Implemented |
| | `glfwGetRequiredInstanceExtensions` | `glfw.GetRequiredInstanceExtensions()` | Implemented |
| **Vulkan (Surfaces)**| `glfwCreateWindowSurface` | *To be implemented* | Planned |
| **Input & Events** | `glfwSetKeyCallback`, etc. | *To be implemented* | Planned |
| **Monitors & Video** | `glfwGetMonitors`, etc. | *To be implemented* | Planned |
