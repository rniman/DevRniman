# Git Commit Convention

## 🎮 DirectX 12 Git Convention

### ✅ Commit Message Format

```
[TAG] One-line summary (in English, within 50 characters)

- Detailed description 1
- Detailed description 2 (Option)
```

### 📌 Examples

```bash
[Add] Implement command queue and swap chain

[Fix] Prevent crash on window resize
- Caused by uninitialized RTV
- Recreate descriptor heap during resizing

[Refactor] Separate frame resource logic into class

[Docs] Add build instructions to README.md
```

### 📌 Writing Rules

- **Always write in English**
- Write the commit title in **present tense** (e.g., Add, Fix, Refactor)
- Body is optional, written as a list starting with '-'
- The title should be **short and clear**

---

## 🏷️ Commit Tag Types

| Tag | Description |
| --- | --- |
| `[Init]` | Initial project setup, structure creation |
| `[Add]` | Add new feature, class, or file |
| `[Update]` | Modify or improve existing feature |
| `[Fix]` | Bug fix |
| `[Remove]` | Delete code, resource, or feature |
| `[Refactor]` | Refactoring (improving structure without changing behavior) |
| `[Optimize]` | Performance optimization |
| `[Docs]` | Add or update documentation |
| `[Chore]` | Configuration, dependencies, and other maintenance tasks |
| `[Test]` | Add or update test code |

---

## 🔀 Branch Naming Rules

```
<Type>/<Brief-Description>
```

- All branch names are **case**, **kebab-case**
- Use a clear prefix (type) according to the purpose of the work

| Type | Description | Example |
| --- | --- | --- |
| `feature/` | New feature development | `feature/weapon-system` |
| `bugfix/` | Common Bug fix | `bugfix/camera-clip-issue` |
| `refactor/` | Code refactoring | `refactor/player-input` |
| `hotfix/` | Urgent fix before release | `hotfix/loading-screen-bug` |
| `release/` | Release preparation | `release/v1.0.0` |
| `test/` | Experimental or test work | `test/lighting-tweak` |
| `docs/` | Documentation work | `docs/update-readme` |
| `chore/` | Configuration files, build, and other tasks | `chore/update-gitignore` |

> ❗ hotfix/ and release/ are usually based on main or release branch
>

*This convention serves as a guideline to improve commit history tracking and overall project maintainability in the DX12 game engine project.*