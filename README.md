# Multi-Container Runtime

A lightweight Linux container runtime in C with a long-running supervisor and a kernel-space memory monitor.

Read [`project-guide.md`](project-guide.md) for the full project specification.

---

## Getting Started

### 1. Fork the Repository

1. Go to [github.com/shivangjhalani/OS-Jackfruit](https://github.com/shivangjhalani/OS-Jackfruit)
2. Click **Fork** (top-right)
3. Clone your fork:

```bash
git clone https://github.com/<your-username>/OS-Jackfruit.git
cd OS-Jackfruit
```

### 2. Set Up Your VM

You need an **Ubuntu 22.04 or 24.04** VM with **Secure Boot OFF**. WSL will not work.

Install dependencies:

```bash
sudo apt update
sudo apt install -y build-essential linux-headers-$(uname -r)
```

### 3. Run the Environment Check

```bash
cd boilerplate
chmod +x environment-check.sh
sudo ./environment-check.sh
```

Fix any issues reported before moving on.

### 4. Prepare the Root Filesystem

```bash
mkdir rootfs-base
wget https://dl-cdn.alpinelinux.org/alpine/v3.20/releases/x86_64/alpine-minirootfs-3.20.3-x86_64.tar.gz
tar -xzf alpine-minirootfs-3.20.3-x86_64.tar.gz -C rootfs-base

# Make one writable copy per container you plan to run
cp -a ./rootfs-base ./rootfs-alpha
cp -a ./rootfs-base ./rootfs-beta
```

Do not commit `rootfs-base/` or `rootfs-*` directories to your repository.

### 5. Understand the Boilerplate

The `boilerplate/` folder contains starter files:

| File                   | Purpose                                             |
| ---------------------- | --------------------------------------------------- |
| `engine.c`             | User-space runtime and supervisor skeleton          |
| `monitor.c`            | Kernel module skeleton                              |
| `monitor_ioctl.h`      | Shared ioctl command definitions                    |
| `Makefile`             | Build targets for both user-space and kernel module |
| `cpu_hog.c`            | CPU-bound test workload                             |
| `io_pulse.c`           | I/O-bound test workload                             |
| `memory_hog.c`         | Memory-consuming test workload                      |
| `environment-check.sh` | VM environment preflight check                      |

Use these as your starting point. You are free to restructure the repository however you want — the submission requirements are listed in the project guide.

### 6. Build and Verify

```bash
cd boilerplate
make
```

If this compiles without errors, your environment is ready.

### 7. GitHub Actions Smoke Check

Your fork will inherit a minimal GitHub Actions workflow from this repository.

That workflow only performs CI-safe checks:

- `make -C boilerplate ci`
- user-space binary compilation (`engine`, `memory_hog`, `cpu_hog`, `io_pulse`)
- `./boilerplate/engine` with no arguments must print usage and exit with a non-zero status

The CI-safe build command is:

```bash
make -C boilerplate ci
```
---------------------------------------------------------------------------------
---

# **Operating Systems - Jackfruit**
*OUTPUT SCREENSHOTS*

---------------------------------------------------------------------------------
***Screenshot 1***
1Multi-container Supervision
<img width="897" height="250" alt="Screenshot 2026-04-17 143004" src="https://github.com/user-attachments/assets/67981880-3a8e-4c7c-8fa2-d2cd4223ace2" />


---------------------------------------------------------------------------------
***Screenshot 2***
Metadata Tracking
<img width="908" height="255" alt="Screenshot 2026-04-17 143018" src="https://github.com/user-attachments/assets/20aa3b3a-13e6-4d16-9d36-74b41c4238a4" />


---------------------------------------------------------------------------------
***Screenshot 3***
3. Bounded-Buffer Logging

<img width="904" height="711" alt="Screenshot 2026-04-17 143100" src="https://github.com/user-attachments/assets/5a6e2046-3c06-4619-9d2c-70bd606cf027" />


---------------------------------------------------------------------------------
***Screenshot 4***
4. CLI and IPC
<img width="905" height="155" alt="Screenshot 2026-04-17 143222" src="https://github.com/user-attachments/assets/b3c3b08e-2831-451c-ac48-1637f2970ddd" />


---------------------------------------------------------------------------------
***Screenshot 5***
Soft-Limit Warning
<img width="894" height="244" alt="image" src="https://github.com/user-attachments/assets/814e4bf5-07b8-4956-b7fd-f64b7a1169a5" />



---------------------------------------------------------------------------------
***Screenshot 6***
6. Hard-Limit Kill
<img width="890" height="496" alt="Screenshot 2026-04-17 143428" src="https://github.com/user-attachments/assets/64a1b11b-e56d-424d-9c2e-cf097a01aa13" />


---------------------------------------------------------------------------------
***Screenshot 7***
Scheduling experiment (cpu-high log)
<img width="1141" height="661" alt="Screenshot 2026-04-17 143817" src="https://github.com/user-attachments/assets/c3c8113b-d833-4f2b-a06a-6517620e1039" />


---------------------------------------------------------------------------------
***Screenshot 8***
Scheduling experiment (cpu-low log)
<img width="1086" height="673" alt="Screenshot 2026-04-17 143858" src="https://github.com/user-attachments/assets/7b405acc-f254-43f8-8d13-07cfaeb5b90e" />




---------------------------------------------------------------------------------
***Screenshot 9***
Clean teardown
<img width="1242" height="512" alt="Screenshot 2026-04-17 144325" src="https://github.com/user-attachments/assets/4b81940d-9ac1-435c-bcf1-5234b520354e" />




---------------------------------------------------------------------------------

