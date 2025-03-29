# Installing MicroCap on Linux with Wine

This guide will walk you through installing MicroCap (electronic circuit simulation software) on Linux using Wine. This allows you to run this Windows application on your Linux system with desktop integration and file access.

## Prerequisites

- A Linux distribution (Ubuntu, Fedora, Arch, etc.)
- Internet connection
- Basic familiarity with terminal commands

## Step 1: Install Wine

First, you need to install Wine on your Linux system. The commands vary depending on your distribution:

### Ubuntu/Debian
```bash
sudo apt update
sudo apt install wine winetricks
```

### Fedora
```bash
sudo dnf install wine winetricks
```

### Arch Linux
```bash
sudo pacman -S wine winetricks
```

Verify Wine is installed correctly:
```bash
wine --version
```

## Step 2: Configure Wine (Optional but Recommended)

It's a good idea to configure Wine before installing MicroCap:

```bash
winecfg
```

In the Wine configuration window:
1. Go to the "Applications" tab and add a new application setting for MicroCap (you can do this after installation)
2. Choose Windows 10 as the Windows version
3. In the "Libraries" tab, you may need to add specific DLLs depending on MicroCap's requirements
4. Click "Apply" and "OK"

## Step 3: Download MicroCap

1. Visit the official MicroCap website to download the installer
   - For the evaluation version: http://www.spectrum-soft.com/download/download.shtm
   - For licensed versions, use your provided download link

2. Save the installer to a location you can easily access, such as your Downloads folder

## Step 4: Install MicroCap

Run the installer using Wine:

```bash
cd ~/Downloads  # Or wherever you saved the installer
wine MicroCap12Setup.exe  # Replace with the actual filename
```

Follow the installation wizard:
1. Accept the license agreement
2. Choose the installation directory (the default is usually fine)
3. Select components to install
4. Complete the installation

## Step 5: Create a Desktop Shortcut

Create a .desktop file to easily launch MicroCap from your applications menu or desktop:

```bash
mkdir -p ~/.local/share/applications
```

Create a new file called `microcap.desktop`:

```bash
nano ~/.local/share/applications/microcap.desktop
```

Add the following content (adjust paths as needed):

```
[Desktop Entry]
Name=MicroCap
Comment=Electronic Circuit Simulation
Exec=wine "C:\\Program Files\\Spectrum Software\\Micro-Cap 12\\mc12.exe"
Type=Application
StartupNotify=true
Icon=wine-notepad
Categories=Education;Science;Electronics;
```

Save the file and make it executable:

```bash
chmod +x ~/.local/share/applications/microcap.desktop
```

## Step 6: Add an Icon (Optional)

For a better desktop integration, you can add a custom icon:

1. Download or extract the MicroCap icon from the program files
2. Save it to `~/.local/share/icons/microcap.png`
3. Update the Icon line in your .desktop file to `Icon=microcap`

## Step 7: Configure File Access

Wine automatically mounts your Linux filesystem as the Z: drive. To access your Linux files from MicroCap:

1. Open MicroCap through your new desktop shortcut
2. When opening or saving files, navigate to the Z: drive
3. From there, you can access all your Linux files

For convenience, you can also create symlinks in your Wine C: drive:

```bash
ln -s ~/Documents ~/.wine/drive_c/Documents
```

## Troubleshooting

### MicroCap Won't Start

Try installing additional Windows components:

```bash
winetricks vcrun2015
winetricks dotnet48
```

### Font or Display Issues

Adjust the DPI settings in winecfg:

```bash
winecfg
```

Go to the "Graphics" tab and adjust the DPI settings.

### Performance Issues

Try using a different Wine version through Wine-Staging or Lutris.

## Updating MicroCap

When a new version is released, download the update and install it using Wine just like the initial installation.

## Removing MicroCap

To uninstall MicroCap:

1. Use the Windows uninstaller:
   ```bash
   wine uninstaller
   ```
   
2. Select MicroCap from the list and click "Remove"

3. Delete the desktop file:
   ```bash
   rm ~/.local/share/applications/microcap.desktop
   ```

## Notes for Educational Use

If you're using MicroCap for schoolwork, consider these tips:

1. Create a dedicated folder for your circuit projects in your Linux home directory
2. Configure MicroCap to use this directory as the default save location
3. Remember that file paths in Wine use Windows conventions (backslashes, drive letters)

## Contributing

If you find improvements or have suggestions for this guide, please submit a pull request or open an issue.

## License

This guide is provided under the MIT License.
