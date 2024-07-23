# nx-bug-demo

Project to showcase change in environment variable parsing between nx versions.

## Issue

Consider `.env` file with contents
```
FOO="foo"
BAR="$FOO-bar"
```

Parsing of the variables changes when updating `nx` from 19.2 to 19.3.

## Reproduction
```
npm i
npm run echo
```

Output contains following lines:
```
> nx --output-style=stream exec -- echo $FOO $FOOBAR

foo foo-bar
```

Next, install newer version of nx with
```
npm i nx@19.3
```

Run command again
```
npm run echo
```

Output contains
```
> nx --output-style=stream exec -- echo $FOO $FOOBAR

foo foo
```

Note how suffix is missing from the printed `FOOBAR` variable.
