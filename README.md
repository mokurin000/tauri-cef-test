# Tauri + Vanilla TS

This template should help get you started developing with Tauri in vanilla HTML, CSS and Typescript.

## Shared CEF for Linux

### Installation

```bash
cef_version=$( cat src-tauri/Cargo.lock |
   grep -A 1 'name = "cef"' |
   tail -1 |
   cut -d '"' -f 2 |
   cut -d + -f 2 )
file_name=$( curl -sSL https://cef-builds.spotifycdn.com/index.json |
    tr ' ' '\n' |
    grep "${cef_version}" |
    grep linux64_minimal |
    tr -d '",' )

cef_dir="${HOME}/.local/share/cef"

aria2c -x 16 --out "${file_name}" "https://cef-builds.spotifycdn.com/${file_name}"

if ! [ -d 'cef-rs' ]; then
   git clone https://github.com/mokurin000/cef-rs --branch "fix/extract-archive-location" --depth 1 cef-rs
fi

(
   cd cef-rs
   cargo run -p export-cef-dir -- --archive "../${file_name}" --force "${cef_dir}"
)
rm -f "${file_name}"
```

### Update `cef-rs` and libCEF

```bash
(cd src-tauri/ && cargo update)
```

And re-run installation commands.

### Setup environment

```bash
cef_dir="${HOME}/.local/share/cef"

export CEF_PATH="${cef_dir}"
export LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:${CEF_PATH}"
```

## Recommended IDE Setup

- [VS Code](https://code.visualstudio.com/) + [Tauri](https://marketplace.visualstudio.com/items?itemName=tauri-apps.tauri-vscode) + [rust-analyzer](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer)
