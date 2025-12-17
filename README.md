# Tauri + Vanilla TS

This template should help get you started developing with Tauri in vanilla HTML, CSS and Typescript.

## Shared CEF for Linux

### Installation

```bash
cef_dir="${HOME}/.local/share/cef"
file_name=cef_binary_142.0.17+g60aac24+chromium-142.0.7444.176_linux64_minimal.tar.bz2

mkdir -p "${cef_dir}"
curl -Lo "${cef_dir}/${file_name}" "https://cef-builds.spotifycdn.com/${file_name}"
sha1sum=$( sha1sum "${cef_dir}/${file_name}" | cut -d ' ' -f 1 )
cat > "${cef_dir}/archive.json" <<EOF
{
   "name": "$file_name",
   "type": "minimal",
   "sha1": "$sha1sum"
}
EOF
```
### Setup environment

```bash
cef_dir="${HOME}/.local/share/cef"

export CEF_PATH="${cef_dir}"
export LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:${CEF_PATH}"
```

## Recommended IDE Setup

- [VS Code](https://code.visualstudio.com/) + [Tauri](https://marketplace.visualstudio.com/items?itemName=tauri-apps.tauri-vscode) + [rust-analyzer](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer)
