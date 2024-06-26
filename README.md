> [!NOTE]
> This is a fork of [`tsc-files`](https://www.npmjs.com/package/tsc-files) which
> modernizes the whole codebase a bit and implements some unmerged pull requests
> of the [original repository](https://github.com/gustavopch/tsc-files).

# tsc-files

A tiny tool to run `tsc` on specific files without ignoring `tsconfig.json`.

## Why

I wanted to type-check **only the staged files**
with [lint-staged](https://github.com/okonet/lint-staged).

Unfortunately passing specific files like `tsc --noEmit file1.ts file2.ts` will
cause TypeScript to simply ignore your `tsconfig.json`.

There's already an open issue in the TypeScript repo to support this use case —
you may want to give a 👍
there: https://github.com/microsoft/TypeScript/issues/27379

## Installation

```sh
npm install --save-dev @jonasgeiler/tsc-files
```

```sh
yarn add --dev @jonasgeiler/tsc-files
```

```sh
pnpm add --save-dev @jonasgeiler/tsc-files
```

## Usage

With lint-staged:

```json
{
  "lint-staged": {
    "**/*.ts": "tsc-files --noEmit"
  }
}
```

## How it works

For the most part, it just forwards all arguments to `tsc` with one exception:
the specified files will not be forwarded — instead, they will be put at
the `files` property of a temporary config that will be generated next to your
original `tsconfig.json`. Other than that, just read `tsc --help`.
