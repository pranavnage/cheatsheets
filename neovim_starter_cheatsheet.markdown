# Neovim Cheatsheet for Coding & Text Editing

## Modes
- **Normal Mode**: Default for navigation/commands (`Esc` to enter).
- **Insert Mode**: For typing text.
- **Visual Mode**: For selecting text (`v`, `V`, `Ctrl-v`).
- **Command-line Mode**: For commands like `:w` (save), `:q` (quit).

## 1. Movement (Normal Mode)
| Command | Description |
|---------|-------------|
| `h`/`j`/`k`/`l` | Move left/down/up/right |
| `0` | Start of line |
| `$` | End of line |
| `w` | Next word start |
| `b` | Previous word start |
| `gg` | First line of file |
| `G` | Last line of file |
| `:n` | Jump to line `n` (e.g., `:5`) |

**Tip**: Prefix with number (e.g., `3j` = move down 3 lines).

## 2. Selection (Visual Mode)
| Command | Description |
|---------|-------------|
| `v` | Character-wise selection |
| `V` | Line-wise selection |
| `Ctrl-v` | Block-wise selection |
| Move (e.g., `w`, `j`) | Extend selection |
| `Esc` | Exit Visual Mode |

**Example**: `v3w` selects 3 words.

## 3. Copying (Yanking)
| Command | Description |
|---------|-------------|
| `y` | Yank selected text (Visual Mode) |
| `yy` | Yank current line |
| `y$` | Yank to end of line |
| `yw` | Yank to end of word |

**Example**: `3yy` yanks 3 lines.

## 4. Pasting
| Command | Description |
|---------|-------------|
| `p` | Paste after cursor (below for lines) |
| `P` | Paste before cursor (above for lines) |

**Note**: In Visual Mode, `p` overwrites selection.

## 5. Deleting
| Command | Description |
|---------|-------------|
| `d` | Delete selected text (Visual Mode) |
| `dd` | Delete current line |
| `dw` | Delete to end of word |
| `diw` | Delete word under cursor |
| `d$` | Delete to end of line |
| `x` | Delete character under cursor |
| `X` | Delete character before cursor |

**Example**: `3dd` deletes 3 lines.

## 6. Changing Text
| Command | Description |
|---------|-------------|
| `c` | Change selected text (Visual Mode) |
| `cc` | Change current line |
| `cw` | Change to end of word |
| `ci"` | Change inside quotes |
| `s` | Delete character & enter Insert Mode |
| `S` | Delete line & enter Insert Mode |
| `r` | Replace one character |
| `R` | Enter Replace Mode |

**Example**: `cw` deletes word and enters Insert Mode.

## 7. Insert Mode
| Command | Description |
|---------|-------------|
| `i` | Insert before cursor |
| `a` | Insert after cursor |
| `I` | Insert at start of line |
| `A` | Insert at end of line |
| `o` | New line below |
| `O` | New line above |
| `Ctrl-w` | Delete previous word |
| `Ctrl-u` | Delete to start of line |
| `Ctrl-h` | Delete previous character |

## 8. Searching
| Command | Description |
|---------|-------------|
| `/pattern` | Search forward |
| `?pattern` | Search backward |
| `n` | Next match |
| `N` | Previous match |

**Example**: `/foo` then `n` for next "foo".

## 9. Replacing
| Command | Description |
|---------|-------------|
| `:s/old/new/` | Replace first "old" in line |
| `:s/old/new/g` | Replace all "old" in line |
| `:%s/old/new/g` | Replace all "old" in file |

**Example**: `:%s/foo/bar/g` replaces all "foo" with "bar".

## 10. Indentation
| Command | Description |
|---------|-------------|
| `>>` | Indent line right |
| `<<` | Indent line left |
| `=` | Auto-indent line |
| `=G` | Auto-indent to end of file |

**Example**: In Visual Mode, select lines and press `>`.

## 11. Undo/Redo
| Command | Description |
|---------|-------------|
| `u` | Undo last change |
| `Ctrl-r` | Redo last undone change |

## 12. Registers
| Command | Description |
|---------|-------------|
| `"ay` | Yank to register "a" (e.g., `"ayy`) |
| `"ap` | Paste from register "a" |
| `"+y` | Copy to system clipboard |
| `"+p` | Paste from system clipboard |

## 13. Macros
Scripts
| Command | Description |
|------|---------|-------------|
| `q`   | `qa` | Start recording to macro "a" |
| `q`   | Stop recording |
| `s`   | `@a` | Replay macro "a" |

**Example**: `qa dd j q` records deleting a line, then `@a` repeats.

## 14. Marks
| Command | Description |
|---------|-------------|
| `ma` | Set mark "a" |
| `'a` | Jump to mark "a" |

## 15. Windows
| Command | Description |
|---------|---------------------|
| `:split` | Split window horizontally |
| `:vsplit` | Split window vertically |
| `Ctrl-w h/j/k/l` | Move to window (left/down/up/right) |
| `:tabnew` | Open new tab |
| `gt`/`gT` | Next/previous tab |

## Tips
- **Counts**: `3dd` = delete 3 lines.
- **Text Objects**: `diw` (delete inner word), `ci"` (change inside quotes).
- **Repeat**: `.` repeats last change.
- **Help**: `:help` (e.g., `:help dd`).
