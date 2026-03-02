# libmdbx

This repository contains the **libmdbx** library used by ImtCore.

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
