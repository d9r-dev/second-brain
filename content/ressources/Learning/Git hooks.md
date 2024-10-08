---
title: Git hooks
draft: false
publish: true
tags:
  - tooling
date: 2024-09-02
---
- official git hooks documentation [Link](https://git-scm.com/docs/githooks)
- Hooks are programs you can place in a hooks directory to trigger actions at certain points in git’s execution. Hooks that don’t have the executable bit set are ignored.
- git hooks are not part of the repository, that makes them a bit harder to maintain
- Solutions:
	- git-build-hook Maven Plugin [Github](https://github.com/rudikershaw/git-build-hook)
	- [[Husky]] (manage git hooks per package.json) [Husky documentation](https://typicode.github.io/husky/)
- Practical Uses:
- scripts must be executable
	- on Linux for example `chmod +x pre-commit`
- bypass hooks by `--no-verify`
- Ressources:
	- [awesome-git-hooks repository](https://github.com/aitemr/awesome-git-hooks)
	- [Introdcution to Git Hooks](https://www.youtube.com/watch?v=8-JL6NOTZOw)
