---
name: browser-screenshot-with-puppeteer
description: Öffnet die aktuelle Website in einem Browser mit Puppeteer und erstellt Screenshots. Verwende diesen Skill, wenn du den aktuellen Stand einer Website visuell erfassen oder dokumentieren willst.
---


# Browser Screenshot mit Puppeteer

Als docker container läuft neben diesem Container ein chromium browser. Dieser ist unter

`ws://chromium:3000` erreichbar. Das vorbereitete Screenshot-Script nutzt Puppeteer, um diesen Browser zu steuern und Screenshots zu erstellen.

Mach dir keine Gedanken, wo dieser Container her kommt. Er ist da und kann Aufgaben erledigen.

The current project/container is available via hostname "main": So "http://main:4000" can be used to access the current 
container from the chromium container. (Always screenshot port 4000 - 4999 is for internal use only.)

If the screenshot fails, ask the user to check if the stack is available and if kick dev was run.

## Hard rules for agents

- Use only the provided `scripts/screenshot.js` command from this skill.
- Do not write or execute inline Puppeteer scripts. If you need to - ask the user first and prompt why the script is not sufficient.
- If measurements or DOM details are needed, create an HTML snapshot with `--html-output-filename` and inspect that file with normal file-reading tools.

## Parameters

- `--device <desktop|mobile|tablet>`
- `--html-output-filename <datei>` speichert zusätzlich einen HTML-Snapshot des aktuellen DOMs inklusive offenem Shadow DOM von Components.

## Example 

Make screenshot of the current page:

```
node /opt/.pi/skills/infracamp-ai-skills/browser-screenshot-with-puppeteer/scripts/screenshot.js --url http://main:4000 --device desktop --output-filename /tmp/screenshot.png
```

Make screenshot and save DOM + Shadow DOM snapshot:

```
node /opt/.pi/skills/infracamp-ai-skills/browser-screenshot-with-puppeteer/scripts/screenshot.js --url http://main:4000 --device desktop --output-filename /tmp/screenshot.png --html-output-filename /tmp/page-snapshot.html
```


## Hinweise

- Der HTML-Snapshot enthält das aktuelle DOM der Seite und bettet offenes Shadow DOM als declarative Shadow DOM (`<template shadowrootmode="...">`) ein.
- Geschlossene Shadow Roots können technisch nicht ausgelesen werden.

## Don'ts

Do not read additional files unless really needed. Do not write additional code or inline browser automation. Just execute the provided screenshot script.


## Install

Do not install this script on your own. Only when asked by the user.

Install by putting references/.kick-stack.yml into the project root.