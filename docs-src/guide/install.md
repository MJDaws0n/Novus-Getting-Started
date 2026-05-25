# Install Novus and Nox

Novus is the compiler. Nox is the package manager. Install both.

## 1. Install Novus

### Automatic install

```bash
curl -fsSL https://raw.githubusercontent.com/MJDaws0n/novus/main/install.sh | bash
```

### Manual install

Download the correct binary from the [Novus releases page](https://github.com/MJDaws0n/Novus/releases), then put it on your `PATH`.

```bash
sudo cp novus_<your-platform> /usr/local/bin/novus
sudo chmod +x /usr/local/bin/novus

# macOS only
sudo xattr -d com.apple.quarantine /usr/local/bin/novus
```

## 2. Install Nox

Download a Nox release from the [Nox repository](https://github.com/MJDaws0n/Nox/releases), then install it:

```bash
sudo cp nox_download /usr/local/bin/nox
sudo chmod +x /usr/local/bin/nox
sudo xattr -d com.apple.quarantine /usr/local/bin/nox
```

## 3. Verify the tools

```bash
novus
nox help
```

If both commands print help or version text, you are ready to create a project.

## Platform notes

### macOS

- Install Xcode Command Line Tools.
- If Gatekeeper blocks a binary you downloaded manually, clear quarantine with `xattr -d`.

### Linux

Make sure the platform assembler and linker are available for the targets you care about.

### Cross compilation

If you cross-compile, your host still needs the right backend tools. The Novus README is the best place to check exact requirements for:

- `linux/amd64`
- `linux/arm64`
- `linux/386`
- `windows/amd64`
- `darwin/arm64`

## What to do next

After installation, go straight to [Your First Project](first-project.md). That is the fastest way to confirm the whole toolchain works end to end.
