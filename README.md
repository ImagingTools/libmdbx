# libmdbx

This repository contains the **libmdbx** library used by ImtCore.


MSVC VC17 libraries: 
- (currently used) based on master branch's commit hash '3412f1b7bbfe9a80f9e3e8265df389b697d5c273' (28.02.2026).
- based on stable branch's commit hash '0dc7dc8bb0c9111f62857f2668e9d1c512b669c1' (03.04.2026).
- based on stable branch's unknown commit (some point at 2024).

VC16, GCC and macOS:
- (currently used) based on stable branch's unknown commit (some point at 2024).

**Note**:
Pinned to libmdbx commit `b1e34acd5a9232a8d8159ee5317c7d87af5b0467` (v0.14.1-490, 2026-03-22).

Commit `b1e34acd` introduced a search dispatching refactor that added
`cursor_to_search_foliage()`. This function contains an assertion:

    mc->clc->k.lmax == mc->clc->k.lmin && (keylen == 4 || keylen == 8)

This assertion fires on any `MDBX_INTEGERKEY` database when a read or search
is performed before a put (e.g. read-only transactions, or first access on
open). The cause is that `keysize_min(MDBX_INTEGERKEY)` initializes `lmin=4`
while `lmax=8`, and the lazy narrowing introduced in the same commit only
triggers on the write path (`cursor_put`), not on the read/search path.

Track the upstream fix at:
https://gitflic.ru/project/erthink/libmdbx


## Origin

This library was extracted from the ImtCore repository (`3rdParty/libmdbx`) 
to enable independent version control and easier dependency management.

**Note**: This repository uses **Git LFS** (Large File Storage) for binary files (*.dll, *.lib, *.so, *.exe, etc.). Make sure you have Git LFS installed before cloning.

## Usage

This repository is integrated into ImtCore as a git submodule:

```bash
git submodule add https://github.com/ImagingTools/libmdbx.git 3rdParty/libmdbx
```

## Cloning

To clone this repository with LFS files:

```bash
git lfs install  # If not already installed
git clone https://github.com/ImagingTools/libmdbx.git
```

## Updating

To update this library in ImtCore:

1. Make changes in this repository
2. Commit and push changes
3. In ImtCore repository:
   ```bash
   cd 3rdParty/libmdbx
   git pull origin main
   cd ..\..
   git add 3rdParty/libmdbx
   git commit -m "Update libmdbx submodule"
   git push
   ```

## License

See LICENSE file if present, or refer to the original library's licensing terms.
