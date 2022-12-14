# LVGL simulator for windows and vscode

![Running Simulator](running_simulator.png?raw=true "Running Simulator")

The [LVGL](https://github.com/lvgl/lvgl) is written mainly for microcontrollers and embedded systems however you can run the library **on your PC** as well without any embedded hardware.
In this repository, the simulator for LVGL8.0 has been prepared for **windows** and **VSCode** based on the [original](https://github.com/lvgl/lv_port_pc_VSCode) repository which was ready for Linux.

## Requirements

This project is configured for windows and VSCode. You need to install the following tools to compile and debug it:

- **VSCode :** Install the [VSCode](https://code.visualstudio.com/download) as code editor

  - **VSCode Extensions:**
    - [**C/C++**](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools) by Microsoft
    - [**C/C++ Extension Pack**](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools-extension-pack) by Microsoft
    - [**Material Theme**](https://marketplace.visualstudio.com/items?itemName=Equinusocio.vsc-material-theme) by Equinusocio
    - [**Native Debug**](https://marketplace.visualstudio.com/items?itemName=webfreak.debug) by WebFreak
    - [**CodeLLDB**](https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb) by Vadim Chugunov
    - [**Project Manager**](https://marketplace.visualstudio.com/items?itemName=alefragnani.project-manager) by Alessandro Fragnani

- **gcc :** Install gcc by [MinGW](https://www.mingw-w64.org/downloads/#mingw-builds) as the compiler
- **gdb :** Install gdb by MinGW as the debuger
- **make :** Install make as the build system
- **git :** Install [git](https://git-scm.com/download/win) as the source control system

---

## Usage

### Clone the project

Clone the project on your PC by the following command. Just copy the entire command and paste it inside a **CMD (command prompt)** :)

**Note:** make sure to paste it inside a `CMD` terminal, not inside a `git bash terminal`

```
git clone --recursive https://github.com/niaraki/lvgl8.0_simulator_win_vscode.git lvgl_simulator
cd .\lvgl_simulator\source
code .
```

### Build the project

Open the **lvgl_simulator\source** directory inside the vscode and press `ctrl+shift+b` and select `Build` from the opened menu. The build process is started and the final program is created inside the "source\build\bin\" with the name "demo.exe".

**Note**: sdl2.dll should be exist beside of "demo.exe" to execute without any Error.

### Execution

Press **ctrl+shift+b** in VSCode and select **Execute** from the opened menu to execute the simulator.

### Debug

Press `ctrl+shift+d` in VSCode and click on the "Run and Debug" button or press `F5` to start the debuging session.

### Configuration

To allow custom UI code an `lv_conf.h` file placed at `ui/simulator/inc` will automatically override this projects lv_conf.h file. By default code under `ui` is ignored so you can reuse this repository for multiple projects. You will need to place a call from `main.c` to your UI's entry function.
