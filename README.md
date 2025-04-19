# Docker in Python
A rebuilt Docker from scratch using Python. A project to help deepen knowledge on Linux containers.

This repository contains a personal implementation of the [Rubber Docker Workshop](https://github.com/Fewbytes/rubber-docker/tree/master). The implementation follows the workshop's levels and exercises, using the `linux` Python module provided by the workshop and [24.04 ubuntu cloud image](https://cloud-images.ubuntu.com/releases/noble/release/ubuntu-24.04-server-cloudimg-amd64.tar.gz).

## Prerequisites

- Ensure you have the `linux` Python module installed. Follow the [workshop's README](https://github.com/Fewbytes/rubber-docker/tree/master) and slides for installation instructions.
- Cloud/Docker image (like [24.04 ubuntu cloud image](https://cloud-images.ubuntu.com/releases/noble/release/ubuntu-24.04-server-cloudimg-amd64.tar.gz))
- This implementation assumes you have a basic understanding of Linux namespaces, cgroups, and system calls.

## Levels and Test Commands

Each level builds upon the previous one, adding more isolation and control to the container. Below are the test commands for each level to verify the functionality.

### Level 00: Fork and Exec
**Test Command**:
```sh
sudo python3 rd.py run -i ubuntu /bin/bash
```
**Verification**:
- Ensure the container starts and you get a bash shell.

### Level 01: Mount Namespace
**Test Command**:
```sh
sudo python3 rd.py run -i ubuntu /bin/bash
```
**Verification**:
- Check that the mounts inside the container are isolated from the host.

### Level 02: Mount Proc
**Test Command**:
```sh
sudo python3 rd.py run -i ubuntu /bin/bash
```
**Verification**:
- Check that `/proc` is mounted inside the container.

### Level 03: Pivot Root
**Test Command**:
```sh
sudo python3 rd.py run -i ubuntu /bin/bash
```
**Verification**:
- Ensure the root filesystem is correctly pivoted.

### Level 04: Chroot
**Test Command**:
```sh
sudo python3 rd.py run -i ubuntu /bin/bash
```
**Verification**:
- Ensure the container's root filesystem is isolated.

### Level 05: UTS Namespace
**Test Command**:
```sh
sudo python3 rd.py run -i ubuntu /bin/bash -- -c hostname
```
**Verification**:
- The hostname within the container should be different from the host system.

### Level 06: PID Namespace
**Test Command**:
```sh
sudo python3 rd.py run -i ubuntu /bin/bash
```
**Verification**:
- Use `ps` and `ls /proc` to verify that only the container's processes are visible.

### Level 07: Network Namespace
**Test Command**:
```sh
sudo python3 rd.py run -i ubuntu /bin/bash
```
**Verification**:
- Use `ip link` or `ifconfig` to verify that only the loopback interface (`lo`) is visible.

### Level 08: CPU CGroup
**Test Command**:
```sh
sudo python3 rd.py run -i ubuntu --cpu-shares 200 /bin/bash
```
**Verification**:
- Check `/proc/self/cgroup` to verify the container is in a new CPU cgroup.
- Use `top` or `htop` on the host to observe CPU usage.

### Level 09: Memory CGroup
**Test Command**:
```sh
sudo python3 rd.py run -i ubuntu --memory 128m --memory-swap 150m /bin/bash
```
**Verification**:
- Check `/proc/self/cgroup` to verify the container is in a new memory cgroup.
- Use `stress` to generate memory load and observe the behavior.

### Level 10: Setuid
**Test Command**:
```sh
sudo python3 rd.py run -i ubuntu --user 1000:1000 /bin/bash
```
**Verification**:
- Use `id` inside the container to verify the process is running as the specified user.
- Create files and check ownership outside the container.

## Acknowledgments
[Rubber Docker Workshop](https://github.com/Fewbytes/rubber-docker/tree/master).

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
