# Sol Cesto Gold Patcher

Gold-focused patcher for Sol Cesto. The Windows patcher creates a separate patched copy of the game with gold hotkeys.

This is specifically for setting and locking Sol Cesto gold. It is not a general-purpose mod loader or full game editor.

Tested with Sol Cesto `v100.2`.

Download the ready-to-use EXE from the [Releases page](https://github.com/RyanCraighead/sol-cesto-local-patcher/releases).

## Release Files

- `SolCestoPatcher.exe`: self-contained Windows GUI gold patcher.

## Using the Gold Patcher EXE

1. Download `SolCestoPatcher.exe` from [Releases](https://github.com/RyanCraighead/sol-cesto-local-patcher/releases).
2. Run `SolCestoPatcher.exe`.
3. For `Game folder`, select the folder containing `SolCesto.exe` and `package.nw`.
4. Leave `Output folder` as the auto-filled patched folder, or choose your own separate output folder.
5. Set `Money value`. The default is `999`.
6. Click `Create patched build`.
7. Run `SolCesto.exe` from the patched output folder.

The patched game adds gold hotkeys:

- `F8`: set money once.
- `F9`: toggle money lock.

The money lock starts off by default.

## Building the Gold Patcher

From the repository root:

```powershell
dotnet publish .\SolCestoPatcher\SolCestoPatcher.csproj -c Release -r win-x64 --self-contained true -p:PublishSingleFile=true -p:EnableCompressionInSingleFile=true -o .\output\SolCestoPatcher
```

The EXE will be written to:

```text
output\SolCestoPatcher\SolCestoPatcher.exe
```

## Notes

- Use this gold patcher only with a copy of Sol Cesto you control.
- This patcher has been tested on Sol Cesto `v100.2`.
- The patcher does not modify the original game folder; it creates a separate patched copy.
- If the money display changes but purchases still fail, press `F8` after reaching the menu/shop, or enable the `F9` lock.

## Windows SmartScreen

Windows may show `Publisher: Unknown publisher` for downloaded EXE builds because the release EXE is not Authenticode-signed.

To make that Windows prompt show `Craighead Labs`, the EXE must be signed with a trusted code-signing certificate issued to Craighead Labs. Project metadata can set the file's company/product details, but it does not change the SmartScreen publisher line by itself.

## Repository Layout

```text
SolCestoPatcher/          Windows Forms patcher source
README.md                 Usage instructions
LICENSE                   MIT license
```
