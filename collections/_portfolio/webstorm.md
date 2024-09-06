---
title: WebStorm
definition: The smartest JavaScript IDE
tags: IDE
---

## Plugin: Awesome Console

Install [this plugin](https://plugins.jetbrains.com/plugin/7677-awesome-console)
to be able to click on a file path within the console.

## Macro

Setting up a macro which will fix all the linting issues, optimizes the imports
and runs Prettier.

1. StyleLint

   - Setup a file watcher
     ([fix action](https://youtrack.jetbrains.com/issue/WEB-25069) not yet
     supported) with
     - File Type: `SCSS style sheet`
     - Scope: `Current File`
     - Program: `$ProjectFileDir$/node_modules/.bin/stylelint`
     - Arguments: `$FileName$ --fix`
     - Working Dir: `$FileDir$`
     - Advanced Options: None, all deactivated

2. Record macro (Edit > Macros > Start Macro Recording) in this order

   - Action: TsLintFileFixAction (with opened \*.ts file)
   - Action: OptimizeImports
   - Action: ReformatWithPrettierAction
   - Action: FileWatcher.runForFiles (with opened \*.scss file)
   - Action: SaveAll

3. Save macro as e.g. `Fix & Save`

4. Assign Keyboard shortcut `Ctrl` + `S` to macro `Fix & Save` (search for
   macro)
