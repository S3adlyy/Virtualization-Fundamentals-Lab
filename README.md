# 🖥️ Virtualization Fundamentals Lab

> A hands-on virtualization laboratory designed to demonstrate the fundamental concepts of virtualization using VirtualBox and multiple Linux virtual machines.

![Virtualization](https://img.shields.io/badge/Virtualization-Fundamentals-blue)
![VirtualBox](https://img.shields.io/badge/Hypervisor-VirtualBox-orange)
![Linux](https://img.shields.io/badge/Linux-AlmaLinux%20%7C%20Ubuntu%20%7C%20Kali-black)
![Architecture](https://img.shields.io/badge/Architecture-ARM64-green)
![Status](https://img.shields.io/badge/Status-Completed-success)

---

## 📌 Table of Contents

* [Overview](#-overview)
* [Objectives](#-objectives)
* [Technologies](#-technologies)
* [Laboratory Environment](#-laboratory-environment)
* [Architecture](#-architecture)
* [Virtual Machines](#-virtual-machines)
* [Virtualization Concepts](#-virtualization-concepts)
* [Lab Experiments](#-lab-experiments)
* [Virtual Networking](#-virtual-networking)
* [Resource Management](#-resource-management)
* [VM Isolation](#-vm-isolation)
* [Snapshots](#-snapshots)
* [Cloning](#-cloning)
* [VM Export and Portability](#-vm-export-and-portability)
* [Server Consolidation](#-server-consolidation)
* [Virtualization Advantages](#-virtualization-advantages)
* [Virtualization Challenges](#-virtualization-challenges)
* [Virtualization vs Cloud](#-virtualization-vs-cloud)
* [Project Structure](#-project-structure)
* [How to Reproduce](#-how-to-reproduce)
* [Results](#-results)
* [Future Improvements](#-future-improvements)
* [Learning Outcomes](#-learning-outcomes)
* [Author](#-author)

---

# 📖 Overview

This project is a practical implementation of the fundamental concepts of **computer virtualization**.

The objective is to move beyond theoretical definitions and demonstrate virtualization concepts through a real laboratory environment composed of multiple virtual machines running on a single physical computer.

The laboratory was developed using:

* macOS
* VirtualBox
* AlmaLinux
* Ubuntu
* Kali Linux

The project demonstrates how a physical computer can host multiple isolated virtual machines while sharing its CPU, memory, storage, and networking resources.

---

# 🎯 Objectives

The main objectives of this laboratory are to:

* Understand the fundamentals of virtualization.
* Understand the role of a Virtual Machine Monitor (VMM).
* Understand the difference between host and guest operating systems.
* Understand hypervisors.
* Distinguish between Type 1 and Type 2 hypervisors.
* Create and configure virtual machines.
* Allocate virtual CPU and memory resources.
* Understand resource sharing.
* Demonstrate VM isolation.
* Demonstrate virtual networking.
* Configure NAT networking.
* Configure Host-only networking.
* Understand Bridged networking.
* Demonstrate VM snapshots.
* Demonstrate VM cloning.
* Demonstrate VM portability.
* Understand server consolidation.
* Monitor virtualized resources.
* Identify virtualization advantages and challenges.
* Understand the relationship between virtualization and cloud computing.

---

# 🧰 Technologies

| Technology       | Purpose                              |
| ---------------- | ------------------------------------ |
| macOS            | Host operating system                |
| Apple Silicon M1 | Physical hardware                    |
| VirtualBox       | Virtualization platform              |
| AlmaLinux        | Web/server VM                        |
| Ubuntu           | Application/server VM                |
| Kali Linux       | Administration and network testing   |
| Bash             | Automation and system administration |
| nginx            | Web server                           |
| Git              | Version control                      |
| GitHub           | Project hosting                      |

---
Introduction to Virtualization
1. What is Virtualization?

Virtualization is a technology that allows us to create virtual versions of computing resources such as servers, operating systems, networks, storage, and applications.

Instead of using one physical machine for only one operating system or service, virtualization allows the physical resources to be shared between multiple isolated virtual environments.

For example, on my physical Mac, I can use VirtualBox to create several virtual machines:

Physical Machine
       │
       ▼
   VirtualBox
       │
 ┌─────┼─────────┐
 │     │         │
Kali  Ubuntu  AlmaLinux
 VM     VM        VM

Each VM has its own operating system, virtual CPU, RAM, disk, and network interface.

2. Types of Virtualization — What Are We Virtualizing?

There are five major areas where virtualization can be applied:

Desktop virtualization
Server virtualization
Application virtualization
Network virtualization
Storage virtualization
2.1 Desktop Virtualization

Desktop virtualization allows a user's desktop environment and operating system to run in a virtual environment rather than directly on the user's physical device.

The user can access the virtual desktop from another device.

Main types
VDI — Virtual Desktop Infrastructure
RDS — Remote Desktop Services
DaaS — Desktop as a Service

Example:

User device
     │
     ▼
Virtual Desktop
     │
     ▼
Virtualization infrastructure
2.2 Server Virtualization

Server virtualization divides a physical server into multiple isolated virtual servers.

Each virtual machine can run its own operating system independently.

For example:

Physical Server
      │
      ▼
   Hypervisor
 ┌────┼─────┐
 │    │     │
VM1  VM2   VM3
Linux Windows Linux
Main types
Full virtualization
Paravirtualization
OS-level virtualization
2.3 Application Virtualization

Application virtualization allows an application to run in a virtual or isolated environment without requiring the application to be traditionally installed and integrated with the host operating system.

The application can be delivered to or accessed by a user from another system.

2.4 Network Virtualization

Network virtualization creates logical networks independently of the underlying physical network infrastructure.

Instead of configuring every physical networking device individually, network resources can be created and managed logically through software.

Example:

Physical Network
       │
       ▼
Network Virtualization
       │
 ┌─────┼─────┐
 │     │     │
Net 1 Net 2 Net 3
SDN — Software-Defined Networking

SDN is a software-based approach to managing networks.

It separates network control and management from the physical networking hardware, making networks more programmable and easier to manage.

2.5 Storage Virtualization

Storage virtualization combines physical storage resources and presents them as logical storage resources.

For example:

Physical Storage
 ┌────┬────┬────┐
 │Disk│Disk│Disk│
 └────┴────┴────┘
        │
        ▼
 Storage Virtualization
        │
        ▼
 Logical Storage Pool
SDS — Software-Defined Storage

Software-Defined Storage (SDS) manages storage resources through software and abstracts the physical storage hardware from applications and users.

3. How Are We Virtualizing?

Another way to classify virtualization is according to how the virtualization is implemented.

The main approaches include:

Partitioning
Full virtualization
Software-based virtualization
Hardware-assisted virtualization
Paravirtualization
Hybrid virtualization
Container-based virtualization
3.1 Partitioning

Partitioning divides physical resources into multiple logical environments.

Each environment can operate independently.

The idea can be represented as:

Physical Resources
       │
       ▼
 ┌─────┼─────┐
 │     │     │
Part1 Part2 Part3
3.2 Full Virtualization

In full virtualization, the virtual machine presents virtual hardware to the guest operating system.

The guest OS does not need to know that it is running inside a virtual machine.

For example:

Guest OS
   │
Virtual Hardware
   │
Hypervisor
   │
Physical Hardware

VirtualBox can be used for this type of virtualization.

3.3 Software-Based Virtualization

Software-based virtualization performs virtualization primarily through software techniques such as binary translation.

The virtualization software emulates or translates certain operations between the guest operating system and physical hardware.

This can introduce additional processing overhead.

3.4 Hardware-Assisted Virtualization

Modern processors provide hardware virtualization extensions that help hypervisors run virtual machines efficiently.

Examples include:

Intel VT-x
AMD-V

The basic idea is:

Virtual Machine
      │
      ▼
Hypervisor
      │
      ▼
CPU virtualization extensions
      │
      ▼
Physical CPU

KVM, Hyper-V, VMware ESXi, and other modern hypervisors can use hardware-assisted virtualization.

3.5 Paravirtualization

In paravirtualization, the guest operating system is aware that it is running in a virtualized environment.

The guest OS can communicate with the hypervisor using virtualization-aware interfaces.

This can reduce some virtualization overhead.

Xen supports paravirtualization.

3.6 Hybrid Virtualization

Hybrid virtualization combines concepts from full virtualization and paravirtualization.

The guest OS can run largely as an unmodified operating system while using paravirtualized drivers or interfaces for particular operations, especially I/O.

3.7 Container-Based Virtualization

Containerization provides isolated application environments without requiring a complete guest operating system for every application.

A container packages an application together with its dependencies.

Examples:

Docker
Podman

The architecture is different from traditional VMs:

Traditional VMs:

VM1        VM2        VM3
 │          │          │
OS         OS         OS
 └──────────┼──────────┘
        Hypervisor
            │
       Host Hardware

Container architecture:

Container1 Container2 Container3
     │          │          │
     └──────────┼──────────┘
             Host OS
                │
             Hardware

Containers are generally lighter than complete virtual machines because they share the host operating system's kernel.

4. Hypervisor / Virtual Machine Manager

A hypervisor, also called a Virtual Machine Monitor (VMM), is software or firmware responsible for creating, running, and managing virtual machines.

The hypervisor manages resources such as:

CPU
RAM
Storage
Network interfaces
Virtual hardware
VM lifecycle

For example:

Physical Hardware
       │
       ▼
   Hypervisor
       │
 ┌─────┼─────┐
 │     │     │
 VM1   VM2   VM3

The hypervisor allocates physical resources to each VM.

5. Two Main Types of Hypervisors
5.1 Type 1 — Bare-Metal Hypervisor

A Type 1 hypervisor runs directly on the physical hardware.

There is no conventional host operating system underneath the hypervisor.

VM1     VM2     VM3
 │       │       │
 └───────┼───────┘
     Hypervisor
          │
    Hardware

Examples include:

VMware ESXi
Microsoft Hyper-V
Xen
KVM-based virtualization environments

Type 1 hypervisors are commonly used in servers and data centers.

5.2 Type 2 — Hosted Hypervisor

A Type 2 hypervisor runs as an application on top of a host operating system.

VM1       VM2       VM3
 │         │         │
 └─────────┼─────────┘
       VirtualBox
           │
       Host OS
           │
       Hardware

Examples include:

VirtualBox
VMware Workstation
VMware Fusion
Your current setup

You are using:

MacBook
   │
macOS
   │
VirtualBox
   │
 ┌─┼──────────────┐
 │ │              │
Kali Ubuntu   AlmaLinux

Therefore, VirtualBox is a Type 2 hosted hypervisor in your setup.

6. Open-Source Virtualization Projects

Some important virtualization technologies include:

Technology	Main concept
KVM	Linux-based virtualization
VirtualBox	Hosted virtualization
Xen	Full virtualization and paravirtualization
QEMU	Machine emulation / virtualization support
Docker	Containerization
Podman	Containerization
7. KVM

KVM — Kernel-based Virtual Machine — is a Linux kernel virtualization technology.

When KVM is enabled, the Linux kernel provides the core virtualization infrastructure.

KVM commonly works together with QEMU.

Virtual Machines
       │
       ▼
     QEMU
       │
       ▼
      KVM
       │
       ▼
Linux Kernel
       │
       ▼
Physical Hardware

KVM takes advantage of CPU virtualization extensions such as:

Intel VT-x
AMD-V
8. VirtualBox

VirtualBox is a desktop virtualization platform that allows us to create and run virtual machines on a host operating system.

In our practical laboratory, we use VirtualBox to create:

                    MacBook
                       │
                     macOS
                       │
                   VirtualBox
                       │
          ┌────────────┼────────────┐
          │            │            │
        Kali        Ubuntu       AlmaLinux

Each VM can have its own:

CPU
RAM
Virtual disk
Network adapter
Operating system
Services
9. Our Practical Virtualization Laboratory

For the practical part, we use three virtual machines:

VM	Operating System	Role
VM 1	Kali Linux	Security and network testing
VM 2	Ubuntu	Linux server / testing
VM 3	AlmaLinux	Server / Nginx

We can connect the VMs using a VirtualBox NAT Network.

For example:

             VirtualBox
                  │
            NAT Network
        192.168.100.0/24
                  │
       ┌──────────┼──────────┐
       │          │          │
     Kali       Ubuntu    AlmaLinux
  .100.4       .100.5      .100.6

This allows the VMs to communicate with each other while maintaining network isolation from the physical network.

# 💻 Laboratory Environment

## Physical Host

The laboratory is executed on:

```text
Device: MacBook Air
CPU: Apple M1
Architecture: ARM64
Host OS: macOS
Virtualization Platform: VirtualBox
```

The physical machine provides the hardware resources that are shared among the virtual machines.

---

# 🖥️ Virtual Machines

The laboratory contains three main virtual machines.

| VM       | Operating System | Role                               |
| -------- | ---------------- | ---------------------------------- |
| VM-WEB   | AlmaLinux ARM64  | Web server                         |
| VM-APP   | Ubuntu ARM64     | Application/server environment     |
| VM-ADMIN | Kali Linux ARM64 | Administration and network testing |

### VM-WEB — AlmaLinux

Main responsibilities:

* Web server
* nginx deployment
* Linux administration
* Resource monitoring

### VM-APP — Ubuntu

Main responsibilities:

* Application/server environment
* VM-to-VM communication
* Service testing
* Network experiments

### VM-ADMIN — Kali Linux

Main responsibilities:

* Network testing
* Connectivity testing
* Administration
* Security-oriented laboratory experiments

---

# 🏗️ Architecture

The general laboratory architecture is:

```text
                         ┌──────────────────────┐
                         │      MacBook M1      │
                         │   Physical Hardware  │
                         └──────────┬───────────┘
                                    │
                                    ▼
                              ┌───────────┐
                              │   macOS   │
                              │ Host OS   │
                              └─────┬─────┘
                                    │
                                    ▼
                              ┌───────────┐
                              │ VirtualBox│
                              │ Hypervisor│
                              └─────┬─────┘
                                    │
               ┌────────────────────┼────────────────────┐
               │                    │                    │
               ▼                    ▼                    ▼
        ┌─────────────┐      ┌─────────────┐      ┌─────────────┐
        │  AlmaLinux  │      │   Ubuntu    │      │    Kali     │
        │   VM-WEB    │      │   VM-APP    │      │  VM-ADMIN   │
        ├─────────────┤      ├─────────────┤      ├─────────────┤
        │    nginx    │      │ Application │      │ Network     │
        │ Web Server  │      │ / Services  │      │ Testing     │
        └─────────────┘      └─────────────┘      └─────────────┘
               │                    │                    │
               └────────────────────┼────────────────────┘
                                    │
                            Virtual Network
```

---

# 🧠 Virtualization Concepts

## Physical Machine

The physical machine is the real computer that provides:

* CPU
* RAM
* Storage
* Network interfaces

In this laboratory, the physical machine is a MacBook Air M1.

---

## Host Operating System

The host operating system runs directly on the physical hardware.

```text
Physical Hardware
        ↓
      macOS
        ↓
    VirtualBox
```

---

## Guest Operating System

A guest operating system runs inside a virtual machine.

Examples in this laboratory:

* AlmaLinux
* Ubuntu
* Kali Linux

---

## Virtual Machine

A virtual machine is an isolated software environment that behaves like a physical computer.

Each VM has virtual:

* CPU
* RAM
* Storage
* Network interface
* Hardware devices

---

## Virtual Machine Monitor

The Virtual Machine Monitor, also called a VMM, manages communication between virtual machines and the underlying physical resources.

In this laboratory:

```text
Physical Hardware
        ↓
      macOS
        ↓
    VirtualBox
        ↓
      VMs
```

---

# 🔬 Lab Experiments

## Experiment 1 — System Information

Each virtual machine was inspected using Linux system commands.

### Architecture

```bash
uname -m
```

### Kernel

```bash
uname -r
```

### CPU

```bash
lscpu
```

### Memory

```bash
free -h
```

### Storage

```bash
lsblk
```

### Network interfaces

```bash
ip addr
```

These commands were used to identify the virtual hardware presented to each guest operating system.

---

# Experiment 2 — Resource Allocation

Each VM receives a configurable amount of virtual resources.

Example:

```text
VM-WEB
 ├── 1 vCPU
 ├── 1 GB RAM
 └── 20 GB virtual disk

VM-APP
 ├── 1 vCPU
 ├── 1 GB RAM
 └── 20 GB virtual disk

VM-ADMIN
 ├── 1 vCPU
 ├── 2 GB RAM
 └── 20 GB virtual disk
```

The exact values depend on the available resources of the physical host.

The experiment demonstrates how physical resources can be divided and assigned to multiple virtual machines.

---

# Experiment 3 — Web Server Deployment

AlmaLinux was configured as a virtual web server.

## Install nginx

```bash
sudo dnf update -y
sudo dnf install nginx -y
```

Enable and start nginx:

```bash
sudo systemctl enable --now nginx
```

Check the service:

```bash
sudo systemctl status nginx
```

Test locally:

```bash
curl localhost
```

This demonstrates that a virtual machine can provide a real server role.

---

# Experiment 4 — VM Isolation

Each virtual machine maintains its own:

* Filesystem
* Processes
* Users
* Network configuration
* Operating system

For example, a file created inside AlmaLinux:

```bash
touch ~/alma-secret.txt
```

is not automatically visible from Ubuntu or Kali.

The experiment demonstrates filesystem and process isolation between virtual machines.

---

# Experiment 5 — Virtual Networking

VirtualBox provides multiple networking modes.

The laboratory experiments with:

* NAT
* Host-only
* Bridged

---

# 🌐 Virtual Networking

## NAT

NAT allows a virtual machine to access external networks through the host.

```text
VM
 │
 ▼
Virtual NAT
 │
 ▼
macOS
 │
 ▼
Router
 │
 ▼
Internet
```

Example connectivity test:

```bash
ping 8.8.8.8
```

---

# Host-only Networking

Host-only networking creates a private network between the host and virtual machines.

Example:

```text
                    Host
                     │
                vboxnet0
                     │
          ┌──────────┼──────────┐
          │          │          │
          ▼          ▼          ▼
       AlmaLinux   Ubuntu      Kali
       .56.10      .56.11      .56.12
```

Example network:

```text
192.168.56.0/24
```

The virtual machines can communicate with each other through the virtual network.

Connectivity can be tested using:

```bash
ping <VM-IP>
```

---

# Bridged Networking

Bridged networking connects the virtual machine to the physical network through the host's network interface.

Conceptually:

```text
VM
 │
 ▼
VirtualBox
 │
 ▼
Physical Network Adapter
 │
 ▼
Router / LAN
 │
 ▼
Network
```

This allows a VM to behave more like another device on the physical LAN.

---

# 🧪 VM-to-VM Communication

Example:

```text
AlmaLinux
192.168.56.10
      │
      │ ping
      ▼
Ubuntu
192.168.56.11
```

Test:

```bash
ping 192.168.56.11
```

From Kali:

```bash
ping 192.168.56.10
```

The experiment demonstrates communication through a virtual network.

---

# 📸 Screenshots

The `screenshots/` directory contains evidence of the experiments.

Recommended screenshots:

```text
01-virtualbox-vms.png
02-almalinux-system.png
03-ubuntu-system.png
04-kali-system.png
05-network-configuration.png
06-vm-connectivity.png
07-nginx.png
08-snapshot.png
09-clone.png
```

Screenshots provide visual evidence that the laboratory was actually performed.

---

# 💾 Snapshots

Snapshots were used to save the state of a virtual machine before performing potentially destructive experiments.

Example:

```text
VM-WEB
  │
  ├── Working State
  │
  └── Snapshot
       "Before Experiment"
```

After modifying the VM, the snapshot can be restored.

This demonstrates:

* VM state preservation
* Recovery
* Encapsulation
* Experimental rollback

---

# 🧬 VM Cloning

A virtual machine can be cloned to create another VM based on an existing configuration.

Example:

```text
             VM-WEB
                │
                ▼
          Full Clone
                │
                ▼
        VM-WEB-CLONE
```

Cloning demonstrates:

* Rapid deployment
* VM portability
* Encapsulation
* Infrastructure replication

---

# 📦 VM Export and Portability

Virtual machines can be exported as virtual appliances.

For example:

```text
VM-WEB
   │
   ▼
Export Appliance
   │
   ▼
VM-WEB.ova
```

The exported appliance can be transferred and imported into another compatible virtualization environment.

This demonstrates the portability property of virtualization.

---

# 📊 Resource Monitoring

Linux tools were used to monitor resources.

## CPU

```bash
top
```

or:

```bash
lscpu
```

## Memory

```bash
free -h
```

## Storage

```bash
lsblk
```

## Network

```bash
ip addr
```

## Host monitoring

macOS Activity Monitor was used to observe the resources consumed by VirtualBox and the running virtual machines.

---

# 🔥 Resource Contention Experiment

Virtualization allows several VMs to share physical resources.

However, excessive resource consumption can create contention.

For example:

```text
Physical CPU
     │
     ├── VM-WEB
     ├── VM-APP
     └── VM-ADMIN
```

A CPU-intensive process inside one VM can increase the overall host workload.

Example test:

```bash
yes > /dev/null
```

Stop the process:

```bash
pkill yes
```

The experiment demonstrates the importance of resource allocation and monitoring.

---

# 🏢 Server Consolidation

One of the major motivations for virtualization is server consolidation.

## Traditional infrastructure

```text
Physical Server 1
       ↓
Web Server

Physical Server 2
       ↓
Application Server

Physical Server 3
       ↓
Monitoring Server
```

This can result in underutilized hardware.

## Virtualized infrastructure

```text
              One Physical Host
                     │
                 VirtualBox
                     │
        ┌────────────┼────────────┐
        ▼            ▼            ▼
      VM-WEB       VM-APP      VM-ADMIN
```

Several services can therefore be consolidated onto fewer physical machines.

---

# ✅ Advantages Demonstrated

The laboratory demonstrates several advantages of virtualization.

## Resource Optimization

Physical CPU, memory, storage, and networking resources can be shared among multiple VMs.

## Isolation

VMs are isolated from one another.

## Flexibility

New VMs can be created without purchasing additional physical hardware.

## Fast Deployment

Existing VMs can be cloned or exported.

## Snapshots

VM states can be saved and restored.

## Portability

Virtual machines can be exported and transferred.

## Server Consolidation

Multiple workloads can run on a smaller number of physical machines.

---

# ⚠️ Virtualization Challenges

Virtualization also introduces challenges.

## Resource Contention

Several VMs compete for the same physical resources.

## Host Failure

If the physical host fails, all VMs running on it can become unavailable.

```text
Physical Host Failure
        ↓
 ┌──────┼──────┐
 VM-WEB VM-APP VM-ADMIN
        ↓
   All affected
```

## Storage Consumption

Virtual disks and snapshots can consume significant storage capacity.

## Configuration Complexity

Managing multiple VMs, networks, storage resources, and configurations increases infrastructure complexity.

## Performance Overhead

Virtualization introduces additional layers between workloads and physical hardware.

---

# ☁️ Virtualization vs Cloud Computing

Virtualization and cloud computing are related but are not the same concept.

## Virtualization

Virtualization abstracts physical resources into virtual resources.

Examples:

* Virtual machines
* Virtual CPUs
* Virtual memory
* Virtual disks
* Virtual networks

## Cloud Computing

Cloud computing provides computing resources and services through a network using characteristics such as on-demand provisioning, resource pooling, scalability, and service-based delivery.

Therefore:

```text
Virtualization
      ↓
Technology
```

while:

```text
Cloud Computing
      ↓
Service / Delivery Model
```

Virtualization can be an enabling technology for cloud infrastructure, but virtualization by itself does not constitute a cloud.

---

# 🧩 Project Structure

```text
virtualization-fundamentals-lab/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── docs/
│   ├── virtualization-concepts.md
│   ├── architecture.md
│   ├── networking.md
│   ├── snapshots-cloning.md
│   └── results.md
│
├── diagrams/
│   ├── architecture.png
│   └── network-topology.png
│
├── scripts/
│   ├── system-info.sh
│   ├── network-test.sh
│   └── resource-monitor.sh
│
├── configs/
│   ├── almalinux/
│   ├── ubuntu/
│   └── kali/
│
└── screenshots/
    ├── 01-virtualbox-vms.png
    ├── 02-almalinux-system.png
    ├── 03-ubuntu-system.png
    ├── 04-kali-system.png
    ├── 05-network-configuration.png
    ├── 06-vm-connectivity.png
    ├── 07-nginx.png
    ├── 08-snapshot.png
    └── 09-clone.png
```

---

# 🚀 How to Reproduce

## 1. Requirements

The laboratory requires:

* ARM64-compatible computer
* VirtualBox with Apple Silicon support
* ARM64 Linux ISO images
* At least 6–8 GB available RAM
* Sufficient disk space for virtual machines

## 2. Create the VMs

Create three virtual machines:

```text
VM-WEB
VM-APP
VM-ADMIN
```

Install:

```text
AlmaLinux
Ubuntu
Kali Linux
```

respectively.

## 3. Configure Resources

Example configuration:

```text
VM-WEB
1 vCPU
1 GB RAM
20 GB disk

VM-APP
1 vCPU
1 GB RAM
20 GB disk

VM-ADMIN
1 vCPU
2 GB RAM
20 GB disk
```

Actual values can be adjusted according to available host resources.

## 4. Configure Networking

Configure:

```text
Adapter 1 → NAT
Adapter 2 → Host-only
```

Use a host-only network such as:

```text
192.168.56.0/24
```

## 5. Test Connectivity

Use:

```bash
ip addr
```

and:

```bash
ping <VM-IP>
```

## 6. Deploy nginx

On AlmaLinux:

```bash
sudo dnf install nginx -y
sudo systemctl enable --now nginx
```

Test:

```bash
curl localhost
```

---

# 📈 Results

The laboratory successfully demonstrated the fundamental principles of virtualization.

| Concept                   | Status |
| ------------------------- | ------ |
| Virtual Machine Creation  | ✅      |
| Host / Guest Architecture | ✅      |
| Virtual CPU               | ✅      |
| Virtual Memory            | ✅      |
| Virtual Storage           | ✅      |
| Resource Sharing          | ✅      |
| VM Isolation              | ✅      |
| NAT Networking            | ✅      |
| Host-only Networking      | ✅      |
| Bridged Networking        | ✅      |
| VM-to-VM Communication    | ✅      |
| Snapshots                 | ✅      |
| VM Cloning                | ✅      |
| VM Export                 | ✅      |
| Server Consolidation      | ✅      |
| Resource Monitoring       | ✅      |
| Virtualization Challenges | ✅      |
| Virtualization vs Cloud   | ✅      |

---

# 🎓 Learning Outcomes

After completing this laboratory, I gained practical experience with:

* Virtual machine deployment
* Virtual hardware configuration
* Linux system administration
* Hypervisor concepts
* Resource allocation
* VM isolation
* Virtual networking
* NAT
* Host-only networking
* Bridged networking
* VM snapshots
* VM cloning
* VM portability
* Server consolidation
* Resource monitoring
* Virtualization limitations

The laboratory also provided a foundation for studying:

```text
Virtualization Fundamentals
          ↓
Server Virtualization
          ↓
Storage Virtualization
          ↓
Network Virtualization
          ↓
Containerization
          ↓
Cloud Infrastructure
```

---

# 🔮 Future Improvements

This project is designed to evolve with future virtualization and cloud infrastructure studies.

Planned extensions include:

### Chapter 2 — Server Virtualization

* Multi-server architecture
* VM templates
* Server monitoring
* Service deployment
* VM resource optimization

### Chapter 3 — Storage Virtualization

* Virtual storage pools
* NFS
* iSCSI
* RAID concepts
* Shared storage
* Storage performance testing

### Chapter 4 — Network Virtualization

* VLANs
* Virtual switches
* Routing
* Firewalling
* Network segmentation
* Network isolation

### Chapter 5 — Containerization

* Docker
* Podman
* Containers
* Container images
* Container networks
* Volumes
* Docker Compose

### Cloud Infrastructure

Future experiments may include:

* KVM
* libvirt
* Open vSwitch
* OpenStack
* Infrastructure as Code
* Cloud automation

---

# 📚 Course Alignment

This project directly supports the concepts studied in the **Cloud and Virtualization** course.

### Chapter 1 — Virtualization Fundamentals

Covered topics:

* Definition and principles
* Virtual machines
* VMM
* Hypervisors
* Host and guest systems
* Virtualization properties
* Virtualization history
* Virtualization applications
* Virtualization techniques
* Advantages
* Challenges
* Virtualization and cloud computing

### Future Chapters

The same laboratory will be extended to cover:

* Server virtualization
* Storage virtualization
* Network virtualization
* Containerization

---

# 👨‍💻 Author

**Wassim Saadli**

Computer Science Engineering Student

Areas of interest:

* Cloud Computing
* DevOps
* DevSecOps
* Linux
* Virtualization
* Infrastructure
* Cybersecurity

---

# 📄 License

This project is licensed under the MIT License.

See the `LICENSE` file for more information.

---

⭐ If this project is useful, feel free to explore, fork, or adapt the laboratory for educational purposes.
