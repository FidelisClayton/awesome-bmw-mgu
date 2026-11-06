# Contributing

Thanks for helping. This list is only useful if its labels are right, so every entry is checked against the project itself, not against its repository description.

## What belongs here

- Apps, tools and guides for BMW head units running the MGU (iDrive 7 or iDrive 8).
- The project's source, or at least its packages, on a public page you can link to.
- **Forks and copies only when they say what they add.** A fork whose README is the original's, with nothing of its own described, is left out: link the original instead. Describe only what the fork adds.

## What doesn't

- Anything that ships BMW software: the SDK, firmware, or packages built with the SDK inside. Build instructions are fine; the SDK comes from the reader's own head unit.
- Tools for generating or bypassing BMW feature activation codes (FSC), or anything else that unlocks paid features.
- Projects that collect credentials, or that you can't link to.

## Entry format

```markdown
- [owner/repo](https://github.com/owner/repo) - What it does on the car, in one or two sentences. Anything a reader must know before installing. `📱 app` `🚗 car-tested` (which car) `ID7`
```

- Name the link `owner/repo`, so readers see who publishes it.
- Start the description with a capital letter and end it with a full stop, then the labels.
- Put it in one section only, the one that fits its main purpose. Mention its other apps in the description.

## How to pick the labels

Take each label from the project's own README, manifests and catalog. If you can't find the evidence, leave the label out, or use `❓ untested?` for the test status.

| Label | Use it when |
|---|---|
| `📱 app` | The project publishes an OAP app (`apps/` in `mgu-repo.json`, or `"kind": "app"` in its catalog). |
| `🔓 root tool` | It publishes its own tool (`native/<id>/component.json`, `tools` in `mgu-repo.json`, `"kind": "tool"` in its catalog, or an installer that puts a service on the head unit). Tools run as root. An app that only needs another project's tool, such as cluster-render, doesn't get this label: that tool's own entry has it. |
| `✍️ changes the car` | It patches a BMW program or file, writes coding, or sends commands (not only read requests) to a control unit. |
| `🌐 internet` | It needs an internet connection in the car to work, not only to be installed. |
| `🚗 car-tested` | Its README says it ran on a real car. Add the car in brackets when the README names it, and `(partly)` when only part of it worked. |
| `🧪 not car-tested` | Its README says it ran only on a bench unit, in an emulator or on a PC. |
| `❓ untested?` | Its README doesn't say. |
| `📦 no source` | The repository has packages but not their source. |
| `ID7` `ID8` | From `mguHmi`, or from the README when the manifest doesn't say. |

## The Caution section

Use it for facts that could hurt someone who adds a source without looking, such as a source that publishes its own builds under another project's tool ids, or root tools with no source. State what you found and where, without guessing at intent, and consider telling the project's author.

## Keeping it current

- When you check or re-check entries, update the date near the top of the README.
- A weekly workflow searches GitHub for new MGU projects and lists them in an issue labelled `discovery`. Add each one to the README, or add it to [`.github/discover-ignore.txt`](.github/discover-ignore.txt) if it doesn't belong, so it isn't suggested again.
- Another workflow checks the links every week and on every pull request.

## Pull requests

- One pull request per project, or per correction.
- Say where you found the evidence for each label: a README line, a manifest or a catalog entry.
- Check that the README still renders and the links work.
