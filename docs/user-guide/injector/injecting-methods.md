# Injection Methods in Packet Ripper

Packet Ripper offers various injection methods, each designed to inject code or DLLs into target processes for the purpose of intercepting and manipulating network traffic.

### IM_LoadLibraryExW
- **Description**: Injects a DLL into the target process using the `LoadLibraryExW` Windows API function.
- **Methodology**: Creates a remote thread in the target process, calling `LoadLibraryExW` with the DLL path.
- **Advantages**:
  - Widely supported and compatible with various Windows versions.
  - Less likely to be detected by antivirus software due to common usage.

### IM_LdrLoadDll
- **Description**: Injects a DLL into the target process using the `LdrLoadDll` Windows API function.
- **Methodology**: Utilizes the process environment block (PEB) to locate `LdrLoadDll` and calls it to load the DLL.
- **Advantages**:
  - Less likely to be detected by antivirus software compared to `LoadLibraryExW`.
  - Provides more control over the injection process.

### IM_LdrpLoadDll
- **Description**: Injects a DLL into the target process by directly calling the internal function `LdrpLoadDll`.
- **Methodology**: Bypasses documented API functions and directly calls internal Loader functions.
- **Advantages**:
  - Provides deeper control and customization over the injection process.
  - Less likely to be detected by traditional antivirus software.

### IM_LdrpLoadDllInternal
- **Description**: Injects a DLL into the target process by manually mapping it into memory and invoking internal Loader functions.
- **Methodology**: Offers a manual approach to bypassing documented API functions entirely.
- **Advantages**:
  - Offers the highest level of control and customization over the injection process.
  - Can bypass certain security mechanisms by avoiding documented API functions.

### IM_ManualMap
- **Description**: Manually maps a DLL into the target process's memory space without relying on the Windows Loader.
- **Methodology**: Parses the DLL file manually, resolves dependencies, and maps sections into memory.
- **Advantages**:
  - Completely bypasses the Windows Loader, making it highly stealthy and difficult to detect.
  - Provides full control over the injection process, including custom memory allocation and relocation.

## Summary

Each injection method in Packet Ripper offers unique advantages for injecting code or DLLs into target processes, providing users with flexibility and control over the injection process. From leveraging standard Windows API functions to bypassing the Windows Loader entirely, Packet Ripper's injection methods cater to diverse use cases and security requirements.
