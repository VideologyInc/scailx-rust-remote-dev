# Rust remote Development

This repository contains a simple Rust project that can be built and run on an embedded device (e.g., RPI, OpenWrt) using the CodeLLDB extension.
There are 2 options for developing rust applications for embedded devices:
- vscode remote development
    - vscode, rust-compiler and debugger runs on target
    - Tooling is simple as there is no cross compilation
- remote LLDB/GDB-server
    - vscode, rust compiler and debugger runs on host-PC.
    - lldb/gdb-server runs on target device.
    - Tooling is more complex as it requires cross compilation and setup of lldb-server on the target device.
    - Compilation is faster as it runs on the host-PC.

This repository provides a simple example of remote lldb development.


# Development:

- On Host-PC, install rust and cargo:
    ```bash
    curl https://sh.rustup.rs -sSf | sh
    ```
- On Host-PC, install vscode CodeLLDB extension:

    https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb

- On Host-PC, install gcc-arm cross sompiler (gcc-13 or lower)
    ```bash
    sudo apt install gcc-12-aarch64-linux-gnu
    ```
- Configure rust to use this cross compiler:
    ```bash
    rustup target add aarch64-unknown-linux-gnu
    ```
    
- Try to build for target:
    ```bash
    cargo build --target aarch64-unknown-linux-gnu
    ```

- On device, install lldb-server:
    ```bash
    opkg install lldb-server
    ```

- On device, start lldb-server (will run automatically on workspace startup):
    ```bash
    lldb-server platform --listen --server *:17777
    ```
