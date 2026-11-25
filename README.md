# 🍷 Sherry

**S**eamless **H**ypervisor **E**nvironment **R**untime **R**ela**Y**

> *"Sherry is to Wine what WSL2 is to WSL1."*

---

## 🎯 Goal

Sherry intends to bring WSL(+g) user experience to Linux desktop users - Real OS, Integrated desktop user experience.

Sherry itself will be just a thin host wrapper around QEMU-KVM and `virtio-vsock`. The actual guest-side work will be handled by **PORT** (**P**ersistent **O**S **R**elay **T**erminal), a Windows service running inside the VM that brokers user sessions, ConPTY, and RDP RAIL (RemoteApp).

### Key Features

* **Minimial & Native architecture:** Communicates directly over `vsock`.
* **"Subsystem" experience - Seamless terminal & GUI:** Drop into a Windows shell from your Linux terminal, and launch GUI apps as native Wayland windows via RDP RAIL.
* **Both Independent and Session-Persistent Shell & GUI Integration:** Either launch a single shell, or create and attach to active Windows user sessions where launching a GUI binary (e.g., `calc.exe`) from shell seamlessly pops up as a native Wayland window via RDP RAIL.
* **Flexible Desktop modes:** Switch between seamless RemoteApp windows and a full Windows desktop environment whenever needed.

---

## 🚀 Usage Examples (DRAFT)

### Open a user shell (like `wsl -u`)
Connects to `PORT` over `vsock` and spawns a shell over ConPTY as user `aaa`:

    sherry [--user] [aaa]

### Start a session & attach with seamless GUI support
PORT initialises a real "session" with interactive desktop over RDP (with RAIL support), alongside terminal then attaches your terminal:

    sherry --session [aaa]



    sherry --attach aaa

(One unique session per user is currently assumed)

Running a GUI app inside that shell opens it as a standalone Wayland window on your Linux desktop:

    PS C:\Users\aaa> calc.exe

### Attach to the full Windows desktop
If you need the entire Windows desktop environment instead of single RemoteApp windows:

    sherry --session [aaa] [--desktop]
    sherry --attach aaa --desktop

---

## 📄 Legal & License
You should bring your own license for Windows VM, obviously.

I am not currently sure whether this project is against any kind of license, so license for this project is not determined for now.