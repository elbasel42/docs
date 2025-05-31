# Glow

Simply run `glow` without arguments to start the textual user interface and
browse local. Glow will find local markdown files in the
current directory and below or, if you’re in a Git repository, Glow will search
the repo.

Markdown files can be read with Glow's high-performance pager. Most of the
keystrokes you know from `less` are the same, but you can press `?` to list
the hotkeys.

## The CLI

In addition to a TUI, Glow has a CLI for working with Markdown. To format a
document use a markdown source as the primary argument:

```bash
# Read from file
glow README.md

# Read from stdin
echo "[Glow](https://github.com/charmbracelet/glow)" | glow -

# Fetch README from GitHub / GitLab
glow github.com/charmbracelet/glow

# Fetch markdown from HTTP
glow https://host.tld/file.md
```

### Word Wrapping

The `-w` flag lets you set a maximum width at which the output will be wrapped:

```bash
glow -w 60
```

### Paging

CLI output can be displayed in your preferred pager with the `-p` flag. This defaults
to the ANSI-aware `less -r` if `$PAGER` is not explicitly set.

### Styles

You can choose a style with the `-s` flag. When no flag is provided `glow` tries
to detect your terminal's current background color and automatically picks
either the `dark` or the `light` style for you.

```bash
glow -s [dark|light]
```

Alternatively you can also supply a custom JSON stylesheet:

```bash
glow -s mystyle.json
```

For additional usage details see:

```bash
glow --help
```

Check out the [Glamour Style Section](https://github.com/charmbracelet/glamour/blob/master/styles/gallery/README.md)
to find more styles. Or [make your own](https://github.com/charmbracelet/glamour/tree/master/styles)!

## The Config File

If you find yourself supplying the same flags to `glow` all the time, it's
probably a good idea to create a config file. Run `glow config`, which will open
it in your favorite $EDITOR. Alternatively you can manually put a file named
`glow.yml` in the default config path of you platform. If you're not sure where
that is, please refer to `glow --help`.

Here's an example config:

```yaml
# style name or JSON path (default "auto")
style: "light"
# mouse wheel support (TUI-mode only)
mouse: true
# use pager to display markdown
pager: true
# at which column should we word wrap?
width: 80
# show all files, including hidden and ignored.
all: false
```


