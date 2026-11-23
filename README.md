# Open Archive MCP

Open Archive is a local Model Context Protocol (MCP) server that builds Motorola MOTOTRBO CPS codeplugs from Excel channel matrices. This release supports the R7 UHF and XPR 7550e UHF.

## Download

Choose the bundle for your computer from the [latest release](https://github.com/ryanonmars/open-archive-downloads/releases/latest). Each bundle includes Node.js, the .NET helpers, and starter codeplugs for both radios.

| Computer | File ending |
| --- | --- |
| Windows with an Intel or AMD processor | `win-x64.tar.gz` |
| Windows with an ARM processor | `win-arm64.tar.gz` |
| Mac with Apple Silicon | `osx-arm64.tar.gz` |
| Mac with an Intel processor | `osx-x64.tar.gz` |

On Windows, check **Settings → System → About → System type** if you are unsure. On Mac, choose **Apple menu → About This Mac** and look for **Chip** or **Processor**.

## Install on Windows

1. Open PowerShell in the folder containing the download.
2. Run the commands below. Replace the filename if you downloaded the ARM64 bundle or a newer version.

   ```powershell
   $archive = "open-archive-0.1.0-win-x64.tar.gz"
   $install = Join-Path $env:LOCALAPPDATA "OpenArchive"
   New-Item -ItemType Directory -Force -Path $install | Out-Null
   tar -xf $archive -C $install
   $mcp = Join-Path $install ($archive -replace '\.tar\.gz$', '')
   ```

3. Register the server with your MCP client from the same PowerShell window. Run the command for your client.

   **Codex CLI**

   ```powershell
   codex mcp add open_archive -- "$mcp\bundle\bin\node.exe" "$mcp\src\mcp.js"
   ```

   **Claude Code**

   ```powershell
   claude mcp add --scope user --transport stdio open_archive -- "$mcp\bundle\bin\node.exe" "$mcp\src\mcp.js"
   ```

## Install on Mac

1. Open Terminal in the folder containing the download.
2. Run the commands below. Replace the filename if you downloaded the Intel bundle or a newer version.

   ```sh
   archive=open-archive-0.1.0-osx-arm64.tar.gz
   install="$HOME/OpenArchive"
   mkdir -p "$install"
   tar -xf "$archive" -C "$install"
   mcp="$install/${archive%.tar.gz}/open-archive-mcp"
   ```

3. Register the server with your MCP client from the same Terminal window. Run the command for your client.

   **Codex CLI**

   ```sh
   codex mcp add open_archive -- "$mcp"
   ```

   **Claude Code**

   ```sh
   claude mcp add --scope user --transport stdio open_archive -- "$mcp"
   ```

## Connect another MCP client

Open `INSTALL.md` in the extracted bundle for an example `mcpServers` configuration for Qwen Code and other local stdio MCP clients. Use absolute paths to the executable and arguments in the extracted bundle.

## Test your install

Start a new agent session and ask **“Use Open Archive MCP to list the radio profiles.”** Both the R7 UHF and XPR 7550e UHF profiles should appear.

The MCP reads matrices from the `matrices` subfolder and saves codeplugs to the `output` subfolder of your local profile. The profile is `%USERPROFILE%\.open-archive` on Windows and `~/.open-archive` on Mac. Follow `INSTALL.md` to set your local Wi-Fi credentials for event builds. You can open the generated files in Motorola CPS to review and write them to the radio.
