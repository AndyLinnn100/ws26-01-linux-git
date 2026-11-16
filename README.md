# ws26-01-linux-git: Linux basics and Git

- Time: 2026-11-18 (Wed) 18:30–20:00 (HKT). The room will be announced on site.
- Organization home: [hkust-asc](https://github.com/hkust-asc)
- Internal guides: [WSL](https://github.com/hkust-asc/.github-private/blob/main/docs/wsl-setup.md) · [SSH / VS Code](https://github.com/hkust-asc/.github-private/blob/main/docs/ssh-vscode.md) · [Git conventions](https://github.com/hkust-asc/.github-private/blob/main/docs/git-rules.md)

Goal: finish the quests below and open a pull request on this private repository with your profile (and any tokens from quests you completed).

## Git conventions (required)

1. Use the branch `submit/<your-github-id>` (or `fix/<your-github-id>-<short-description>` for a bug fix). Do not push to `main` directly.
2. Put your files under `submissions/<your-github-id>/` (for example, `submissions/yourid/profile.md`). Do not edit anyone else’s folder, and do not edit the original files in `quests/`.
3. Write commit messages that say what you did. Do not use `update`, `111`, or `asdf`.
4. Pull request title: `[Submit] Your Name (@github-id)`. Issue title: `[Bug] filename: short description` or `[Question] description of the problem`.

```bash
git clone https://github.com/hkust-asc/ws26-01-linux-git.git
cd ws26-01-linux-git
git checkout -b submit/<your-github-id>
mkdir -p submissions/<your-github-id>
```

## Quest 1: Log into the remote node and set up ranger (~20 minutes)

SSH details are in the “Server access” section on the internal organization home page (to be filled in by the coach). After you connect:

1. Run `pwd` to see where you are, create a `workspace` directory, and `cd` into it.
2. Without `sudo`, install `ranger` in your home directory and add an alias:

```bash
git clone https://github.com/ranger/ranger.git ~/.ranger
echo "alias ranger='python3 ~/.ranger/ranger.py'" >> ~/.bashrc
source ~/.bashrc
```

3. Start `ranger`, browse `/opt/asc_quest/` with the arrow keys, then press `q` to quit.

## Quest 2: I/O redirection and tmux (~25 minutes)

1. Run `/opt/asc_quest/noisy_sensor.sh`. Run it again from `~/workspace`, sending standard output (stdout) to `passcode.txt` and standard error (stderr) to `error.log`.
   - Check: `cat passcode.txt` should show only one clean `PASSCODE` line, with no `[ERROR]` text.
2. `tmux` disconnect protection:
   - Start a session named `sim` with `tmux new -s sim`.
   - Inside it, run `/opt/asc_quest/long_sim.sh` (about 60 seconds).
   - While it is still running, press `Ctrl+B`, release, then press `D` to detach. You may even disconnect SSH.
   - After about a minute, reconnect, run `tmux ls`, and check the Token in `~/sim_result.txt` in your home directory.

(The coach will place these two scripts on the server at `/opt/asc_quest/`. They are not in this Git repository.)

## Quest 3: Git branches and a pull request (~30 minutes)

You can do this on the server, on local WSL / macOS / Linux, or in VS Code Remote-SSH.

1. Configure your Git identity and GitHub login ( `gh auth login` is a good option).
2. Clone this repository and switch to your branch `submit/<your-github-id>`.
3. In `submissions/<your-github-id>/profile.md`, include:
   - Your name / year and major
   - The `PASSCODE` and Token from Quest 2 (if the server is not open yet, submit the profile first and add the tokens later)
   - One or two areas on the Map of HPC that interest you most
4. Commit, push, and open a pull request on GitHub titled `[Submit] Your Name (@github-id)`.

## Quest 4 (bonus): for those who finish early

`quests/matmul_buggy.c` is a broken C matrix-multiplication program. It contains a bug.

1. Open the file and find which line is wrong and why. You may use VS Code / Copilot, but you should understand the bug yourself.
2. **Do not fix this file and push it to `main`.** Open an issue titled `[Bug] matmul_buggy.c: short description`, and explain what you found, which line it is on, and how you would fix it.

## Layout

- `slides/`, `demos/`: class materials (added when available)
- `quests/`: starter files for the exercises
- `submissions/<your-github-id>/`: your work
