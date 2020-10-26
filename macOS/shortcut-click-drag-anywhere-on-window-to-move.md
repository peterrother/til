# Ctrl-command-click & drag in macOS windows to move them

## Install

Run the following in terminal:

```
defaults write -g NSWindowShouldDragOnGesture -bool true
```

## Uninstall

Run the following in terminal:

```
defaults delete -g NSWindowShouldDragOnGesture
```
