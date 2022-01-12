`gcci` allows to run C files as scripts, omitting the compilation step
(actually hiding it).  Most importantly, modified file still remains
a valid C code and can be compiled by normal means.

Example usage:
```
$ cat hello.c
#include <stdio.h>
int main() {
  printf("Hello world!\n");
  return 0;
}

# Insert "shebang"
$ gcci -i hello.c

# Run!
$ ./hello.c
Hello world!
```

You can also execute without instrumentation:
```
$ gcci hello.c
Hello world!
```

If you get `gcci: command not found` error in last line, you need to add `gcci` to `PATH`
or use absolute path instead:
```
$ gcci -i -a ...
```

To override default compilation flags (`-Wall -DNDEBUG -O2`) use `--compiler-flags` option
during instrumentation stage:
```
$ gcci -i --compiler-flags='-O0 -w' ...
```

`gcci` is based on a hack from [What's the appropriate Go shebang line?](https://stackoverflow.com/questions/7707178/whats-the-appropriate-go-shebang-line)

TODO:
* add compilation cache (in `$HOME/.gcci`)
