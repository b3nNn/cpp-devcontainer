# cpp-devcontainer

An efficient solution for c++ development under Windows and MacOS.

Recommanded IDE: [IntelliJ](https://www.jetbrains.com/help/idea/dev-containers-starting-page.html), [VSCode](https://code.visualstudio.com/docs/devcontainers/containers).

## Requirements
| Software                                                          | Min. Version |
|-------------------------------------------------------------------|--------------|
| [Docker Desktop](https://www.docker.com/products/docker-desktop/) | 4.38.0       |
| [IntelliJ](https://www.jetbrains.com/idea/)                       | 2024.3.1.1   |
| [VS Code](https://code.visualstudio.com/)                         | 1.97.2       |

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
- [x] Test on Windows with VSCode.
- [ ] Test on MacOS with IntelliJ.
- [ ] Test on MacOS with VSCode.
