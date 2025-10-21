# ExecuteVimMotion Action

The `ExecuteVimMotion` action allows you to bind arbitrary Vim motion sequences to keyboard shortcuts. This works even when Vim mode is disabled, making it useful for accessing specific Vim text objects without having to enable full Vim mode.

## Usage

Add keybindings to your keymap file (e.g., `~/.config/zed/keymap.json`):

```json
{
  "context": "Editor",
  "bindings": {
    "cmd+'": ["vim::ExecuteVimMotion", { "motion": "viq" }]
  }
}
```

## Examples

### Select text inside quotes
Bind `cmd+'` to select text inside quotes (equivalent to `viq` in Vim):

```json
{
  "context": "Editor",
  "bindings": {
    "cmd+'": ["vim::ExecuteVimMotion", { "motion": "viq" }]
  }
}
```

### Delete a word
Bind `cmd+d` to delete the word under the cursor:

```json
{
  "context": "Editor",
  "bindings": {
    "cmd+d": ["vim::ExecuteVimMotion", { "motion": "diw" }]
  }
}
```

### Yank text inside quotes
Bind `cmd+y` to copy text inside quotes:

```json
{
  "context": "Editor",
  "bindings": {
    "cmd+y": ["vim::ExecuteVimMotion", { "motion": "yiq" }]
  }
}
```

### Select around word
Bind `cmd+shift+w` to select around the word (including surrounding whitespace):

```json
{
  "context": "Editor",
  "bindings": {
    "cmd+shift+w": ["vim::ExecuteVimMotion", { "motion": "vaw" }]
  }
}
```

### Change inside curly brackets
Bind `cmd+shift+b` to change content inside curly brackets:

```json
{
  "context": "Editor",
  "bindings": {
    "cmd+shift+b": ["vim::ExecuteVimMotion", { "motion": "ci{" }]
  }
}
```

## Supported Motion Sequences

The `ExecuteVimMotion` action supports the following Vim commands:

### Mode Switches
- `v` - Enter visual mode (or toggle back to normal)
- `V` - Enter visual line mode (or toggle back to normal)

### Operators
- `i` - Inner text object (excludes delimiters)
- `a` - Around text object (includes delimiters and surrounding whitespace)
- `d` - Delete
- `c` - Change (delete and enter insert mode)
- `y` - Yank (copy)

### Text Objects
- `q` or `'` - Single quotes
- `"` - Double quotes
- `` ` `` - Backticks
- `w` - Word (lowercase for word with punctuation boundaries)
- `W` - WORD (uppercase for whitespace-delimited word)
- `p` - Paragraph
- `s` - Sentence
- `t` - Tag
- `b`, `(`, `)` - Parentheses
- `[`, `]` - Square brackets
- `{`, `}` - Curly brackets
- `<`, `>` - Angle brackets

## Motion Sequence Examples

You can combine operators and text objects to create powerful motion sequences:

- `viq` - Select inside quotes
- `vaw` - Select around word (including trailing space)
- `viw` - Select inside word (excluding trailing space)
- `diw` - Delete inside word
- `ciw` - Change inside word
- `yiq` - Yank (copy) inside quotes
- `ci{` - Change inside curly brackets
- `di(` - Delete inside parentheses
- `ya[` - Yank around square brackets (including the brackets)
- `vip` - Select inside paragraph
- `vis` - Select inside sentence
- `dit` - Delete inside tag

## Notes

- When Vim mode is disabled, the action temporarily creates a Vim context to execute the motion, then restores the original editor state.
- When Vim mode is enabled, the action uses the existing Vim context.
- After executing a motion that enters visual mode (like `viq`), you remain in visual mode with the selection active.
- After executing a delete or change operation, the cursor is positioned according to Vim rules.
