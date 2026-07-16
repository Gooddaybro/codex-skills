# Codex Skills

Personal reusable Codex skills. This GitHub repository is the source of truth; install individual skill directories into `~/.codex/skills`.

## Available Skills

### `learn-project`

Use `learn-project` to understand concepts inside an existing Java, Python, JavaScript, AI, or backend project. It profiles the repository, maps architecture and runtime flow, connects new concepts to prior knowledge, and checks mastery through run, predict, explain, connect, reconstruct, and transfer evidence.

### `learn-coding`

Use `learn-coding` when code is understandable but difficult to write independently. It follows an example-first practice ladder:

```text
complete correct reference example
-> closed-reference rewrite
-> second reconstruction
-> isomorphic transfer
-> changed-constraint refactor
-> project application and interview explanation
```

The first correct example is visible; later target logic remains learner-owned. Initial exercises use an approved project-local learning worktree and stay outside production source. Production migration requires separate approval.

### Using Them Together

`learn-project` finds and explains the project concept. `learn-coding` turns that concept into deliberate implementation practice. Return to the project afterward to integrate and explain design trade-offs.

## Install on macOS or Linux

Clone the source repository:

```bash
git clone git@github.com:Gooddaybro/codex-skills.git ~/codex-skills
mkdir -p ~/.codex/skills
```

Link the skills you want:

```bash
for skill in learn-project learn-coding; do
  ln -sfn "$HOME/codex-skills/$skill" "$HOME/.codex/skills/$skill"
done
```

Update later with:

```bash
git -C ~/codex-skills pull --ff-only
```

Restart Codex after installing or updating.

## Install or Synchronize on Windows

Clone the source repository once:

```powershell
git clone git@github.com:Gooddaybro/codex-skills.git $env:USERPROFILE\codex-skills
```

Pull later updates:

```powershell
git -C $env:USERPROFILE\codex-skills pull --ff-only
```

Mirror each desired skill into the local Codex skill directory:

```powershell
$skills = @('learn-project', 'learn-coding')
foreach ($skill in $skills) {
    $source = "$env:USERPROFILE\codex-skills\$skill"
    $target = "$env:USERPROFILE\.codex\skills\$skill"

    if ((Test-Path $target) -and
        ((Get-Item -Force $target).Attributes -band [IO.FileAttributes]::ReparsePoint)) {
        throw "$target must be a directory copy, not a junction or symlink."
    }

    New-Item -ItemType Directory -Force $target | Out-Null
    robocopy $source $target /MIR /R:2 /W:1
    if ($LASTEXITCODE -ge 8) {
        throw "Skill synchronization failed for $skill with robocopy exit code $LASTEXITCODE."
    }
}
```

`/MIR` removes stale local files and overwrites local skill changes. Edit the GitHub checkout, not the synchronized copy. Restart Codex after synchronization.

## Usage

Invoke one skill explicitly:

```text
$learn-project Explain how state moves through the Agent workflow in this repository.
```

```text
$learn-coding Teach me Java ToolRegistry. Show one complete correct example first, then close it and make me rewrite it.
```

Use both when project understanding and coding practice are needed:

```text
Use $learn-project to locate and explain the recommendation routing flow, then use $learn-coding to train me to reconstruct an equivalent Java router and solve a transfer exercise.
```
