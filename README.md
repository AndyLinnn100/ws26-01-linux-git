# Week 1: Linux basics and Git

**Wednesday, 2026-11-18, 18:30–20:00 (HKT)** · [ASC Team organization](https://github.com/hkust-asc)

Practice navigating a Linux server, separating program output, keeping a session alive, and submitting work through Git. Server access details are still TBD; the coach will post them on the [internal member board](https://github.com/hkust-asc/.github-private#server-access).

Member guides: [WSL setup](https://github.com/hkust-asc/.github-private/blob/main/docs/wsl-setup.md) · [SSH and VS Code](https://github.com/hkust-asc/.github-private/blob/main/docs/ssh-vscode.md) · [Git rules](https://github.com/hkust-asc/.github-private/blob/main/docs/git-rules.md)

## Quest 1: Connect and explore

1. Once the coach provides the host, port, and account, connect to the training server with SSH. See the [SSH guide](https://github.com/hkust-asc/.github-private/blob/main/docs/ssh-vscode.md) for the command.
2. Create and enter your workspace:

   ```bash
   mkdir -p ~/workspace
   cd ~/workspace
   ```

3. Install `ranger` in your home directory without `sudo`, and set up an alias for Bash:

   ```bash
   git clone https://github.com/ranger/ranger.git ~/.ranger
   echo "alias ranger='python3 ~/.ranger/ranger.py'" >> ~/.bashrc
   source ~/.bashrc
   ```

4. Run `ranger /opt/asc_quest/` to explore the directory. Use the arrow keys to navigate and `q` to quit.

## Quest 2: Redirect output and use tmux

The coach will put `noisy_sensor.sh` and `long_sim.sh` on the server in `/opt/asc_quest/`. They are not stored in Git.

1. From `~/workspace`, run the sensor with standard output and standard error sent to separate files:

   ```bash
   cd ~/workspace
   /opt/asc_quest/noisy_sensor.sh > passcode.txt 2> error.log
   cat passcode.txt
   cat error.log
   ```

   The passcode line in `passcode.txt` should be clean, without error messages. Keep the passcode for your profile.
2. Start a session named `sim` and run the simulation inside it:

   ```bash
   tmux new -s sim
   /opt/asc_quest/long_sim.sh
   ```

3. While it runs, press **Ctrl+B**, release both keys, then press **D** to detach. Reconnect to the server if you disconnected, and reattach:

   ```bash
   tmux attach -t sim
   ```

4. Once the simulation finishes, recover the Token from `~/sim_result.txt`:

   ```bash
   cat ~/sim_result.txt
   ```

## Quest 3: Submit a profile

You may use the server, local WSL/macOS/Linux, or VS Code Remote-SSH. If the server is not open yet, submit your profile first and add the Quest 2 results later.

1. Configure your Git identity and authenticate with GitHub in the environment you choose.
2. Clone this repository and make your submission branch. Replace `YOUR_GITHUB_ID` with your GitHub ID:

   ```bash
   git clone https://github.com/hkust-asc/ws26-01-linux-git.git
   cd ws26-01-linux-git
   git switch -c submit/YOUR_GITHUB_ID
   mkdir -p submissions/YOUR_GITHUB_ID
   ```

3. Create `submissions/YOUR_GITHUB_ID/profile.md` with your name, year and major, the Quest 2 passcode and Token when available, and one or two interests from the [Map of HPC](https://github.com/hkust-asc/.github-private#map-of-hpc).
4. Stage your profile, commit it with a descriptive message, and push your branch:

   ```bash
   git add submissions/YOUR_GITHUB_ID/profile.md
   git commit -m "Add workshop profile"
   git push -u origin submit/YOUR_GITHUB_ID
   ```

5. Open a pull request in this repository titled `[Submit] Your Name (@github-id)`.

## Quest 4: Bonus bug report

Inspect `quests/matmul_buggy.c` and identify the bug. Do not push a fix to `main`. Open an issue titled `[Bug] matmul_buggy.c: short description` explaining the problem and your proposed fix.

## Working rules

- Use `submit/<github-id>` for assignments and `fix/<github-id>-<short-description>` for fixes. Do not push to `main`.
- Unless a quest requires editing a shared file, work only under `submissions/<github-id>/`; do not edit the originals in `quests/` or another person's folder.
- Make commit messages describe the change. `update`, `111`, and `asdf` are not allowed.
- Use `[Submit] Your Name (@github-id)` for submission PRs, and `[Bug] filename: short description` or `[Question] description of the problem` for issues.
- Check `git status` before committing. Do not add generated artifacts, logs, datasets, or model weights.

`slides/` and `demos/` hold workshop materials; `quests/` holds exercise files; `submissions/` holds individual work.
