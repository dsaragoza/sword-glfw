# sword-glfw

Idiomatic, low-overhead GLFW bindings for the Sword programming language. This library provides the foundation for window management, OpenGL context creation, and Vulkan surface querying by wrapping the C Foreign Function Interface (FFI).

## Dependencies
The library utilizes Sword's direct dynamic linking via extern "glfw". You do not need to compile GLFW from source alongside your project. Simply ensure that the native GLFW dynamic library (e.g., libglfw.so on Linux, glfw3.dll on Windows, or the Homebrew equivalent on macOS) is available on your host system at runtime.

## Setup

Since Sword resolves packages directly via directory structure, including **sword-glfw** in your project requires no external package managers or complex build configurations.

**Step-by-step installation:**

1. **Clone this repository** to your local machine:
   ```bash
   git clone https://github.com/DiegoSaragozaSilva/sword-glfw.git
   ```
2. **Copy and paste the glfw folder** from the cloned repository into your target Sword project's source tree.


## Quickstart
Below is a classic example of creating a window and running a main event loop with an active OpenGL context:

```
import "glfw"

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

To compile any example from the **examples** folder, compile and run it with:
```
shield examples/example.sword -o example
./example
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
| | `glfwGetRequiredInstanceExtensions` | `glfw.GetRequiredInstanceExtensions()` |Implemented |
| **Vulkan (Surfaces)**| `glfwCreateWindowSurface` | *To be implemented* | Planned |
| **Input & Events** | `glfwSetKeyCallback`, etc. | *To be implemented* | Planned |
| **Monitors & Video** | `glfwGetMonitors`, etc. | *To be implemented* | Planned |
