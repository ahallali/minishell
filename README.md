# minishell

A small Unix shell written in C, inspired by bash. 42 project, built in a team of two with [LilNex](https://github.com/LilNex).

## Features

- Interactive prompt with command history (GNU readline)
- Execution of commands found in `PATH` or given by relative/absolute path
- Pipes: `cmd1 | cmd2 | cmd3`
- Redirections: `<`, `>`, `>>` and heredoc `<<`
- Single and double quotes, handled like bash
- Environment variable expansion (`$VAR`) and exit status (`$?`)
- Signals: `Ctrl-C` shows a new prompt, `Ctrl-D` exits, `Ctrl-\` does nothing
- Built-ins: `echo` (with `-n`), `cd` (including `cd -`), `pwd`, `export`, `unset`, `env`, `exit`

## Build

Requires a C compiler, `make` and the GNU readline library.

```bash
make
./minishell
```

## Example

```bash
minishell$ export NAME=42
minishell$ echo "Hello $NAME" | tr a-z A-Z > out.txt
minishell$ cat << EOF
> heredoc works
> EOF
minishell$ echo $?
```

## How it works

1. **Lexer / tokenizer** splits the input line into words and operators.
2. **Syntax analyzer** rejects invalid input (unclosed quotes, misplaced pipes or redirections).
3. **Expander** replaces variables and removes quotes.
4. **Executor** sets up pipes and redirections, runs built-ins in the shell process when needed, and forks for external commands.

## Project structure

```
src/minishell.c   main loop
src/parser/       lexer, syntax check, expansion, heredoc
src/exec/         execution, pipes, built-ins, signals
libft/            our C utility library
```
