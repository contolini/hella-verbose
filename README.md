# Hella Verbose

Don't just echo a message to stdout -- have your computer say the message out loud. Useful if you step away from your computer to make a sandwich and want to *listen* to the status of a script. Or if you just want to annoy your users.

## Source code

```sh
say() {
    echo "$@"
    if hash espeak 2>/dev/null; then
        echo "$@" | espeak -s 120 2>/dev/null
    elif hash /usr/bin/say 2>/dev/null; then
        /usr/bin/say "$@" 2>/dev/null
    fi
}
```

## Example

```sh
#!/bin/sh

say() {
    echo "$@"
    if hash espeak 2>/dev/null; then
        echo "$@" | espeak -s 120 2>/dev/null
    elif hash /usr/bin/say 2>/dev/null; then
        /usr/bin/say "$@" 2>/dev/null
    fi
}

DEP_DIR=node_modules

# Clear project dependencies.
if [ -d $DEP_DIR ]; then
  say 'Removing project dependency directories...'
  rm -rf $DEP_DIR
fi
say 'Project dependencies have been removed...'
```
