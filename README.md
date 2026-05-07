# Sol Cesto Gold Patcher and Cheat Tables

Gold-focused tools for a local/offline Sol Cesto build. The main download is a Windows gold patcher that creates a separate patched copy of the game with gold hotkeys, and the Cheat Engine tables provide live attached-process gold editing experiments.

This is specifically for setting and locking Sol Cesto gold. It is not a general-purpose mod loader or full game editor.

Download the ready-to-use EXE and `.CT` files from the [Releases page](https://github.com/RyanCraighead/sol-cesto-local-patcher/releases).

## Release Files

- `SolCestoPatcher.exe`: self-contained Windows GUI gold patcher.
- `SolCesto_live_heap_money.ct`: recommended Cheat Engine table for scanning/writing live gold memory.
- `SolCesto_js_bridge_money.ct`: experimental Cheat Engine table that tries to set gold through the NW.js JavaScript runtime.

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

## Using the Gold Cheat Engine Tables

Start Sol Cesto first, then open Cheat Engine and load one of the `.CT` tables from [Releases](https://github.com/RyanCraighead/sol-cesto-local-patcher/releases). Accept the Lua script prompt when Cheat Engine asks.

### Recommended Table

Use `SolCesto_live_heap_money.ct` first. This table is the normal Cheat Engine workflow: attach to the running game, scan for the current gold value, then set or lock the gold candidates.

1. Attach Cheat Engine to the running `SolCesto.exe` process, or activate `Attach to running SolCesto.exe`.
2. Activate `Set gold once - heap scan from current value`.
3. Enter the current visible/current gold value.
4. Enter the target gold value.
5. If a one-time set is not enough, activate `Lock gold - heap scan from current value`.
6. If the first scan misses the real value, use `Batch test gold candidates` and check the in-game shop after each batch.

Use `Stop lock and clear generated records` when done.

### Experimental JS Bridge Table

Use `SolCesto_js_bridge_money.ct` only if you want to try the direct JavaScript-runtime approach for gold.

1. Attach Cheat Engine to the running `SolCesto.exe` process.
2. Activate `Probe JS bridge`.
3. If the probe succeeds, use `Set gold once through JS runtime` or `Lock gold through JS runtime`.
4. If the probe reports `NO_CDP`, the running game is not exposing a DevTools/CDP bridge, so this table cannot reach the JavaScript runtime in that session.

## Notes

- Use these gold tools only with a local/offline copy you control.
- The patcher does not modify the original game folder; it creates a separate patched copy.
- If the money display changes but purchases still fail, press `F8` after reaching the menu/shop, or enable the `F9` lock.
- Cheat Engine heap scanning can touch unrelated memory. If the game behaves strangely after testing candidates, restart the game and try a narrower batch.

## Repository Layout

```text
SolCestoPatcher/          Windows Forms patcher source
cheat-tables/             Cheat Engine tables
README.md                 Usage instructions
LICENSE                   MIT license
```
