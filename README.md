# llvm-pdbutil-builds

Unofficial 64-bit Windows builds of [`llvm-pdbutil`](https://llvm.org/docs/CommandGuide/llvm-pdbutil.html), built from the LLVM trunk.

For using the build (when prerequisites are installed), simply unpack it, run over the desired .pdb file, and profit.  

<h3>Usage examples:</h3>

-  `llvm-pdbutil dump -all your.pdb`  
   Dump most information available from this PDB.

-  `llvm-pdbutil bytes -syms your.pdb`  
   Dump raw bytes of the symbol record substream.

- `llvm-pdbutil -help`  
   Show the main help screen. `-help` is available for each suboption, too.

<h3>Prerequisites:</h3>

- Visual C++ Redistributable for Visual Studio 2015:  
  https://www.microsoft.com/en-us/download/details.aspx?id=48145

- DIA SDK (Debug Interface Access SDK) - bundled with Visual Studio:  
  https://docs.microsoft.com/en-us/visualstudio/debugger/debug-interface-access/debug-interface-access-sdk?view=vs-2017

- Alternatively, if you're missing the DIA SDK, you could instead install the standalone `msdia140.dll` bundled with the `llvm-pdbutil-9.0.0svn-win64-msdiadll64.7z` zip file (see below for instructions).

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
