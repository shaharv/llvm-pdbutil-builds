# llvm-pdbutil-builds

Unofficial 64-bit Windows builds of [`llvm-pdbutil`](https://llvm.org/docs/CommandGuide/llvm-pdbutil.html).

<h3>llvm-pdbutil build instructions:</h3>

- Clone the LLVM monorepo: `git clone https://github.com/llvm/llvm-project.git`
- `cd llvm-project`
- `mkdir build && cd build`
- If not running from Visual Studio console: `set VSINSTALLDIR=<Path to Visual Studio>\`
   - Verify that the folder `%VSINSTALLDIR%\DIA SDK` exists.
   - Path must end with a backslash and must not be surrounded by quotes.
- Configure the build:
  `cmake -G "Visual Studio 15 2017" -A x64 -Thost=x64 -DLLVM_ENABLE_DIA_SDK=ON ../llvm`
- Open `build\LLVM.sln` in Visual Studio
- build the `Tools/llvm-pdbutil` project.

For more details, visit https://llvm.org/docs/GettingStarted.html.
