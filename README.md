# .barebones

Minimal dotfiles for fresh remote machines.

## Setup

```bash
git clone https://github.com/AdamOrmondroyd/.barebones.git ~/.barebones
bash ~/.barebones/.workstation/customize_environment  # installs stow, uv, etc.
cd ~/.barebones && stow .
```

Once stowed, `~/.workstation/customize_environment` runs on every boot, so packages lost with the ephemeral root filesystem are reinstalled automatically. uv lives in `~/.local/bin`, which persists, so it's only installed once.

If `uv` isn't found on first login, `source ~/.profile` (or log in again) to pick up `~/.local/bin`.

## ssh

Seeing as `xterm-ghostty` isn't in most systems' terminfo databases, it's best to just fall back to `xterm-256color`. **Locally**, I've added `shell-integration-features = ssh-env` to `~/.config/ghostty/config`, but `gcloud compute/workstations ssh` doesn't pick this up, so I added

```
Host *
    SetEnv TERM=xterm-256color
```

to the end of `~/.ssh/config`.
