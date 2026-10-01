# AWM Weighbridge - releases

This page holds the downloads for the AWM Weighbridge program, published by AWM Limited, for
Windows and Linux.

- Each entry under **Releases** is one version of the program. The newest is marked **Latest**.
- The program checks this page for updates from its admin menu.
- This repository is for downloads only - the program's source code is not published here.
- The program needs a licence for your PC to run. Installing it does not include one. The
  **demo** needs no licence.

| You want | Windows | Linux |
| --- | --- | --- |
| The program | `WeighbridgeSetup-<version>.exe` | the install command below |
| The demo | `WeighbridgeDemoSetup-<version>.exe` | the install command below, with `--demo` |

The demo is the whole program with a made-up recycling site and its own built-in database, so
there is nothing else to set up. A slider stands in for the weighbridge.

## Windows

Windows 10 or 11 (64-bit). Download the installer from the **Assets** of the latest release and
run it.

Before installing the program (not needed for the demo), read the two short guides, also shown
inside the installer:

- [Installation notes](installation-notes.txt) - the program needs a MySQL server (not installed
  by the installer), and how to set the database up.
- [Licensing guide](licensing-guide.txt) - how to get and install the licence for your PC.

### If Windows warns you about the installer

Your browser or Windows may warn you when you download or run the installer - for example
"isn't commonly downloaded", or "Windows protected your PC" with "Unknown publisher". This is
because the program is new and its installer is not yet digitally signed, so Windows has not
built up a reputation for it. It does not mean anything is wrong with the file.

- **In your browser:** open the download's menu and choose **Keep**, then **Show more**, then
  **Keep anyway**.
- **When running it:** on the "Windows protected your PC" screen, click **More info**, then
  **Run anyway**.

To be sure the file is genuine, only download it from this page, then right-click the file,
choose **Properties**, and open the **Details** tab. The company should read "AWM Limited".

If your antivirus software removes the file instead, restore it from quarantine and allow it, or
contact whoever supplied the program.

## Linux

64-bit PCs (x86_64) running:

- **Ubuntu** 22.04 or newer, **Debian** 12 or newer, **Linux Mint** 21 or newer
- **Arch Linux** and its relatives, such as **CachyOS**, **EndeavourOS** and **Manjaro**

Open a terminal and run one command, as your normal user (not root). It asks for your password
when it installs things.

**The demo:**

```bash
curl -fsSL https://github.com/WillAWMghub/AWMTKS-releases/releases/latest/download/install.sh | bash -s -- --demo
```

**The program:**

```bash
curl -fsSL https://github.com/WillAWMghub/AWMTKS-releases/releases/latest/download/install.sh | bash
```

**The program, with its database on this PC.** This uses the PC's MySQL or MariaDB server if it
has one, or installs MariaDB if not, then creates the program's database and login and connects
the program to it:

```bash
curl -fsSL https://github.com/WillAWMghub/AWMTKS-releases/releases/latest/download/install.sh | bash -s -- --with-database
```

The installer downloads the latest release, checks it against the release's checksums, installs
what the program needs from your system (with apt on Ubuntu, Debian and Mint, and pacman on
Arch), and adds the program to your applications menu. Running the same command again updates
it to the latest version, keeping your settings, licence and data.

On Ubuntu, Debian and Mint you can instead download the `.deb` file from the release's
**Assets** and open it, or install it with `sudo apt install ./awm-weighbridge_<version>_amd64.deb`.

### After installing

- Open **AWM Weighbridge** (or **AWM Weighbridge Demo**) from the applications menu, or run
  `awm-weighbridge` (`awm-weighbridge-demo`) in a terminal.
- The program shows this PC's machine ID the first time it opens: see the
  [Licensing guide](licensing-guide.txt) to get your licence.
- Staff sign-in on a new installation: username **admin**, password **1234**. Change the
  password straight away under **Users**.
- Weighbridge indicators on a serial port (`/dev/ttyUSB0` and similar): the installer gives your
  user access to serial ports. Log out and back in once before using one.
- Smart card readers need the PC/SC service running: `sudo systemctl enable --now pcscd.socket`
- The program's settings, licence, log and data are kept in `~/.local/share/awm-weighbridge`
  (`~/.local/share/awm-weighbridge-demo` for the demo). Automatic backups go to
  `~/Weighbridge Backups`.
- **Check for updates** in the admin menu shows the command that installs the newer version.

### Removing it

```bash
curl -fsSL https://github.com/WillAWMghub/AWMTKS-releases/releases/latest/download/install.sh | bash -s -- --uninstall
```

Add `--demo` at the end to remove the demo instead. Your settings and data in `~/.local/share`
are kept; delete that folder as well to remove them.

### Good to know

- The demo's database uses MariaDB, which the installer adds. On Ubuntu, Debian and Mint,
  MariaDB can't be installed beside MySQL's server, so on a PC that already runs MySQL the demo
  can't start its own database. The installer tells you if this is the case.
- The Linux files attached to each release are the `.deb` packages (Ubuntu, Debian, Mint), the
  `.tar.xz` packages (other systems; the install command uses them on Arch),
  `SHA256SUMS-linux.txt` and `install.sh`.
- `mariadb-<version>.tar.gz` on each release is the source code of the MariaDB database server
  included in the Windows demo, which is free software under the GNU GPL version 2.
