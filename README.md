Demonstration of bug in [Bun](https://bun.sh/)'s shebang parser on files with CRLF line endings accessed through a symbolic link.

To reproduce:

1. Clone this repo
2. `cd bun-shebang-crlf-bug`
3. `bun link` to register the package
4. `bun link bun-shebang-crlf-bug` to create symlinks in `./node_modules`
5. `bunx buncrlfbug` or `bunx --bun buncrlfbug`

Result:

```
/usr/bin/env: ‘node\r’: No such file or directory
error: "buncrlfbug" exited with code 127
```

This is a minimal reproduction of the same problem when running, for example:

```sh
bunx jscodeshift ...
```

because `jscodeshift` ships with CRLF files. Converting the files to LF avoids the problem.

The CRLF issue does not seem to be a problem when symlinks are not involved.
