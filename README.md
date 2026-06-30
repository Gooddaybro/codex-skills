# Codex Skills

This repository stores my personal Codex skills so I can reuse them across Windows and Mac.

## learn-project

`learn-project` is a Codex skill for learning a project by doing, not by passively reading explanations.

It is useful when I want to:

- study an existing codebase step by step
- understand how a technology appears in real project code
- find weak spots in my own explanation
- rebuild a smaller demo after reading the real implementation
- avoid copying code without understanding the core flow

The skill guides Codex to use a learning loop:

1. ask diagnostic questions
2. give a small reading list
3. ask me to explain the code in my own words
4. point out inaccurate or missing ideas
5. ask me to restate the corrected understanding
6. guide me through a small demo one step at a time

It is designed for topics such as Java backend projects, Redis, MyBatis, Spring Boot flows, AI Agent code, LangGraph, RAG, and other project-level technologies.

## Install on Mac

```bash
git clone git@github.com:Gooddaybro/codex-skills.git ~/codex-skills
mkdir -p ~/.codex/skills
ln -s ~/codex-skills/learn-project ~/.codex/skills/learn-project
```

Restart Codex after installing.

## Install on Windows

```powershell
git clone git@github.com:Gooddaybro/codex-skills.git $env:USERPROFILE\codex-skills
New-Item -ItemType Directory -Force $env:USERPROFILE\.codex\skills
New-Item -ItemType Junction -Path $env:USERPROFILE\.codex\skills\learn-project -Target $env:USERPROFILE\codex-skills\learn-project
```

Restart Codex after installing.

## Usage

Mention the skill explicitly:

```text
$learn-project
```

Or ask Codex to help learn a project topic hands-on. Codex can choose this skill when the request matches the skill description.
