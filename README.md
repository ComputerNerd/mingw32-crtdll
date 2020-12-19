# mingw32-crtdll
Arch Linux PKGBUILD files which builds a Mingw32 toolchain which uses CRTDLL.dll instead of MSVCRT.dll.
## Build order.
1. mingw-binutils
2. mingw-winpthreads-dummy-headers
3. mingw-headers-bootstrap
4. mingw-gcc-boostrap
5. mingw-crt-with-headers-bootstrap
6. mingw-gcc
7. mingw-headers-crt-final


## What this does.
Executables and DLLs built with MinGW-w64 may have compatibility problems with older versions of Windows. This toolchain uses the mingw32 CRT which doesn't generate the .tls section allowing LoadLibrary to work on DLLs built using this toolchain. 

In addition libstdc++ is built without widechar support. This cut the DLL size in half and eliminated some functions which exist in MSVCRT.dll but not CRTDLL.

Also libstdc++ is patched to not reference functions which only exist in newer versions of Windows.

