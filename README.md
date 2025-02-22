# cpp-devcontainer

An efficient solution for c++ development under Windows and MacOS.

Recommanded IDE: IntelliJ, VSCode.

## Features
- C++ development stack for CMake projects.
- Docker-in-Docker.

## Docker

### Windows

#### Arguments
<span>-</span>

#### Build

```powershell
docker build -t cpp-devcontainer:latest -f .\docker\devcontainer\Dockerfile .\docker\devcontainer
```

### Linux/OSX

#### Arguments
<span>-</span>

#### Build

```sh
docker build -t cpp-devcontainer:latest -f ./docker/devcontainer/Dockerfile ./docker/devcontainer
```

## Todo
- [x] Test on Windows with IntelliJ.
- [ ] Test on Windows with VSCode.
- [ ] Test on MacOS with IntelliJ.
- [ ] Test on MacOS with VSCode.
