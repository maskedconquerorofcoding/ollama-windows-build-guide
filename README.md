Manual Ollama Build & Server Guide (Windows)
Status: Last Resort / Server Fix Use Case: Installing Ollama when the official installer fails, or running a headless server instance.

⚠️ CRITICAL WARNING: Building from source via go build on Windows usually results in a CPU-only build. Getting GPU (Nvidia/AMD) support requires installing CMake, MSVC, and the CUDA Toolkit, which is very complex. This version will be stable, but slower than the official release.

Prerequisites
Git: Download here.

Go (Golang): Download here. (Version 1.22+ recommended).

GCC Compiler: Required for CGO bindings. Download TDM-GCC.

Select "MinGW-w64/TDM64" during install.

Part 1: Building the Binary
1. Clean Up Ensure no other instances of Ollama are running. Check your taskbar tray and Task Manager to kill ollama.exe.

2. Open PowerShell (Admin) Right-click your Start button and select Terminal (Admin) or PowerShell (Admin).

3. Clone the Repository

PowerShell

git clone https://github.com/ollama/ollama.git
cd ollama
4. Download Dependencies

PowerShell

go mod download
5. Build the Executable This creates the standard binary.

PowerShell

go build .
Note: If you see errors regarding gcc, ensure TDM-GCC is installed and in your system PATH.

Part 2: Configuring for Server Use
This is the most important part for a server. By default, Ollama only listens to itself (localhost). To let other computers connect to this server, you must change the environment variables.

1. Set the Host (Allow External Connections) Run this command in PowerShell to verify the setup (temporary):

PowerShell

$env:OLLAMA_HOST = "0.0.0.0"
0.0.0.0 tells Ollama to listen on all network interfaces, not just localhost.

2. (Optional) Set CORS If you plan to use a Web UI (like Open WebUI) hosted elsewhere to talk to this server:

PowerShell

$env:OLLAMA_ORIGINS = "*"
3. Run the Server Start the backend process:

PowerShell

.\ollama.exe serve
If successful, you will see Listening on [::]:11434.

Part 3: Making it Permanent (Service)
On a server, you don't want to keep a PowerShell window open forever. You can use NSSM (Non-Sucking Service Manager) to run your custom build as a background service.

Download NSSM.

Extract nssm.exe to a folder.

Run: .\nssm.exe install OllamaCustom

Path: Browse to your new ollama.exe file.

Arguments: Type serve.

Environment Tab: Add the following line: OLLAMA_HOST=0.0.0.0

Click "Install Service".

Now your custom Ollama build runs automatically when the server turns on.

Troubleshooting
"Access Denied": Ensure your firewall (Windows Defender Firewall) allows traffic on port 11434.

Slow Performance: As mentioned, this is likely running on your CPU. If you need GPU support on a manual build, you must look into the Ollama Developer Guide regarding "Local Build with CUDA," which requires Visual Studio 2022.
