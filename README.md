# Codex Skills

This repository stores reusable personal Codex skills. The GitHub repository is the source of truth; installed Codex skill directories are synchronized copies.

## learn-project

`learn-project` v2 is an adaptive learning coach for concepts in existing Java, Python, JavaScript, AI, and backend projects. It first profiles the selected repository, its instructions, Git state, build commands, existing learning locations, architecture, and usable data sources.

The learning progression is evidence-driven:

1. inspect the minimum production code and connect the topic to old knowledge;
2. study and predict one minimal standard worked example;
3. implement learner-owned core logic inside assistant-provided plumbing;
4. run, compare, and correct the underlying mental model;
5. reconstruct the core flow with the reference closed;
6. draw learner-first knowledge, runtime, and project-position maps before seeing a reference diagram;
7. transfer the principle to a genuinely changed business scenario.

A topic passes only after all six gates pass: **run, predict, explain, connect, reconstruct, and transfer**. Passing tests alone is not mastery.

The skill supports business-logic-only exercises while still preferring real project data through thin adapters. Deterministic stand-ins are reserved for nondeterministic or distracting dependencies.

## Install on macOS

```bash
git clone git@github.com:Gooddaybro/codex-skills.git ~/codex-skills
mkdir -p ~/.codex/skills
ln -s ~/codex-skills/learn-project ~/.codex/skills/learn-project
```

Restart Codex after installing.

## Install or Synchronize on Windows

The GitHub checkout is the source of truth. For the first install:

```powershell
git clone git@github.com:Gooddaybro/codex-skills.git $env:USERPROFILE\codex-skills
```

For later source updates:

```powershell
git -C $env:USERPROFILE\codex-skills pull --ff-only
```

After validating the source, mirror it into the local Codex skill directory:

```powershell
$source = "$env:USERPROFILE\codex-skills\learn-project"
$target = "$env:USERPROFILE\.codex\skills\learn-project"
if ((Test-Path $target) -and ((Get-Item -Force $target).Attributes -band [IO.FileAttributes]::ReparsePoint)) {
    throw "Target must be a directory copy, not a junction or symlink."
}
New-Item -ItemType Directory -Force $target | Out-Null
robocopy $source $target /MIR /R:2 /W:1
if ($LASTEXITCODE -ge 8) { throw "Skill synchronization failed with robocopy exit code $LASTEXITCODE." }
```

The local Windows Codex path is an exact synchronized copy, not a junction. `/MIR` removes stale local files and overwrites local skill changes, so edit only the source repository. Verify the mirror before relying on it, then restart Codex.

## Usage

Mention the skill explicitly:

```text
$learn-project
```

Or ask Codex to teach a project concept through a worked example, learner-owned demo, reconstruction, architecture mapping, and transfer practice.
