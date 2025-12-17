# Tauri + Vanilla TS

This template should help get you started developing with Tauri in vanilla HTML, CSS and Typescript.

## Shared CEF for Linux

### Installation

```bash
cef_dir="${HOME}/.local/share/cef"
file_name=cef_binary_142.0.17+g60aac24+chromium-142.0.7444.176_linux64_minimal.tar.bz2

aria2c -x 16 --out "${file_name}" "https://cef-builds.spotifycdn.com/${file_name}"
git clone https://github.com/mokurin000/cef-rs --branch "fix/extract-archive-location" --depth 1 cef-rs
(
   cd cef-rs
   cargo run -p export-cef-dir -- --archive "../${file_name}" --force "${cef_dir}"
)
rm -rf cef-rs/
rm "${file_name}"
```
### Setup environment

```bash
cef_dir="${HOME}/.local/share/cef"

export CEF_PATH="${cef_dir}"
export LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:${CEF_PATH}"
```

## Recommended IDE Setup

- [VS Code](https://code.visualstudio.com/) + [Tauri](https://marketplace.visualstudio.com/items?itemName=tauri-apps.tauri-vscode) + [rust-analyzer](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer)
