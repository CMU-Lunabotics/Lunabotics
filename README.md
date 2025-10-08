# Lunabotics

The official NASA Lunabotics GitHub repository for CMU Lunabotics.

[![Lint Check](https://github.com/GOFIRST-Robotics/Lunabotics/actions/workflows/linter_check.yml/badge.svg)](https://github.com/GOFIRST-Robotics/Lunabotics/actions/workflows/linter_check.yml) [![Trufflehog Scan](https://github.com/GOFIRST-Robotics/Lunabotics/actions/workflows/trufflehog_scan.yml/badge.svg)](https://github.com/GOFIRST-Robotics/Lunabotics/actions/workflows/trufflehog_scan.yml)

## Docker Setup
### MAC OS x Apple Silicon 

1. install docker desktop 
2. install devcontainers extension in vscode 
3. Cmd + Shift + P and select "Dev Containers: Rebuild and Open in Dev Containers"
5. once container is up, access vnc server at vnc://localhost:5901
6. Password is "password" (lol)

## Start the Joystick Node with params

```
ros2 run joy joy_node --ros-args --params-file config/joy_node.yaml
```
