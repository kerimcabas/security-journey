# Week 1 — Foundations Setup

Part of an 18-month security research + pentesting roadmap. Week 1's goal: build the workshop, not "learn hacking" yet — a working lab and a public GitHub repo, proof the machine (and I) are ready.

## What I built
- Verified and organized the core toolchain on an Apple Silicon Mac: Homebrew, git, python@3.12, wget, curl, nmap, tmux, tree, jq, htop, coreutils, gh, multipass, colima, docker.
- A public git identity and this repo, pushed with a real commit history and a `.gitignore`.
- A native ARM Ubuntu VM (`multipass`) I can SSH into with a key pair (no password auth).
- Docker running via `colima`, verified with `hello-world`.
- Read-only inspection of my own Mac's security model: SIP, Gatekeeper/code signing, launchd, Keychain.

## Commands that mattered
See the running reference: `Concepts/Linux Cheat Sheet.md` in the vault — pulled directly from each day's log. Highlights: `which` vs. a package manager's own "installed" list (`brew list --versions`, `dpkg -l`) answer two different questions and can legitimately disagree; `man <command>` (and `man git-<subcommand>`) is the one universal, reliable way to look up any tool's options instead of guessing at `--help`/`-h`.

## Real bugs I hit and fixed (not staged — these actually happened)
1. **`$PATH` shadowing:** Anaconda's `bin` directory comes before Homebrew's on this Mac, so `python3`, `curl`, and `jq` all silently resolved to the Anaconda copies instead of the Homebrew ones I'd just installed. Deferred fixing this on purpose — revisiting once the Python weeks (8–10) make it matter.
2. **Wrong git identity:** typed `user.mail` instead of `user.email` in `git config --global` — git silently accepted the bogus key (config files aren't validated) and fell back to an auto-generated `username@hostname` author on my first commit. Fixed with `--unset` + the correct key, then `git commit --amend --reset-author` (safe since nothing had been pushed yet).
3. **Root-owned `~/.config`:** `gh auth login` failed with a permission error because `~/.config` was owned by `root` (leftover from an old `sudo`-run install). Fixed with `sudo chown -R kerim:staff ~/.config`.
4. **A stray trailing quote** in a `git commit -m "..."` command dropped my shell into a `dquote>` continuation prompt, silently swallowing the next two lines I typed instead of running them as commands — including the `git push` that was supposed to happen.

## What confused me
<!-- fill in: pick 2-3 real moments from the week -->
- some typos cretaed some confusion
- shadow, $PATH 
- 

## Key takeaways
- Technique learned: connecting a device from away phsically by ssh, managing the git repo, creating a virtual linux machine (ubuntu) with ip adress
- Tool learned: virtual machine, git, ssh
- Concept reinforced: basic commands, ls, man, --help, cat, touch etc

## Next
Week 2: Linux fundamentals I (filesystem, navigation, permissions), starting on [[OverTheWire]] Bandit.
