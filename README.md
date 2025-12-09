Local Ollama Build Guide (Windows)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)


⚠️ WARNING: This guide modifies Ollama source code for learning/modding only. It may damage your system—backup data first. Not for hacking/blackhat use. Contact authorities if compromised. Author not liable.​

Prerequisites
GitHub account sign in at github.com

Ollama installed and updated ollama.com/download

8GB+ RAM, decent CPU/GPU recommended

Windows 10/11

Step-by-Step Setup
Fork Ollama repo
Go to github.com/ollama/ollama and click "Fork" (top-right). This creates your copy at github.com/YOUR_USERNAME/ollama.​

Install Git
Download from git-scm.com/downloads. Run installer, select all components on "Select Components" screen for future modding ease.​

Install Go
Download Windows installer from go.dev/dl. Run it (adds go to PATH).​

Open Git Bash
Search "Git Bash" in Start menu and launch.​

Clone your fork

text
git clone https://github.com/YOUR_USERNAME/ollama.git
Replace YOUR_USERNAME with your GitHub username.​

Enter directory

text
cd ollama
Download Go modules

text
go mod download
Verify tools

text
git --version
go version
Both should print versions.​

Build Ollama

text
go build ./...
Wait for compile (may take 5-15 mins).​

Troubleshooting
"go not found"? Restart Git Bash or check PATH.

Build fails? Update Go/Git, ensure fork is latest.

Made by Jedidiah Roberts – For tech learners & modders. Contributions welcome (Apache License 2.0).​​
