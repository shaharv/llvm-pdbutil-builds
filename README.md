# llvm-pdbutil-builds

Unofficial 64-bit Windows builds of [`llvm-pdbutil`](https://llvm.org/docs/CommandGuide/llvm-pdbutil.html), built from the LLVM trunk.

For using the build (when prerequisites are installed), simply unpack it, run over the desired .pdb file, and profit.  

Big shout out to the LLVM team for their hard work on PDB support and this great tool!

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

<h3>msdia140.dll:</h3>

- If you're missing the DIA SDK, you could install the DIA DLL directly:
  1. Unpack `llvm-pdbutil-9.0.0svn-win64-msdiadll64.7z`. 
  2. Register the DLL with: `regsvr32 msdia140.dll`.

- In case the DIA DLL is missing or could not be loaded, the following error may occur:  
  `llvm-pdbutil: An unknown error has occurred. HRESULT: 0x800700C1: Calling NoRegCoCreate`

<h3>llvm-pdbutil build instructions:</h3>

For building `llvm-pdbutil` yourself, follow these steps.

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
