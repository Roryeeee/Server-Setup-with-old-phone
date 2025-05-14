📱 DIY Music Server with an Old Android Phone + External Hard Drive
I turned an old Android phone into a self-hosted music server using open-source tools, a little DIY spirit, and minimal hardware. This project marks my first step into the world of homelabs and self-hosting.

🧩 What I Used
📦 Hardware
Old Android phone (no root required)

External hard drive (for storing music)

Dock with Ethernet, USB, and USB-C ports

Phone stand (for a clean, organized setup)

🛠️ Software
Termux – Terminal emulator and Linux environment for Android

proot-distro – Used to install Ubuntu inside Termux

Navidrome – Lightweight music server

Ultrasonic – Android app to stream music from Navidrome

⚙️ Setup Instructions
1. Install Termux
Download Termux from F-Droid (recommended) or Google Play Store.

2. Install proot-distro and Ubuntu
bash
Copy
Edit
pkg update && pkg upgrade
pkg install proot-distro
proot-distro install ubuntu
proot-distro login ubuntu
3. Set Up Ubuntu Environment
Once inside the Ubuntu shell:

bash
Copy
Edit
apt update && apt upgrade
apt install curl wget unzip
4. Mount the External Hard Drive
Ensure your hard drive is recognized by the phone and mounted in shared storage (accessible via /storage or /mnt in Termux). You may need to allow Termux access to file storage:

bash
Copy
Edit
termux-setup-storage
Then navigate to your mounted drive (e.g., /storage/XXXX-XXXX/Music/).

You can create a symbolic link inside Ubuntu to point to your music folder:

bash
Copy
Edit
ln -s /storage/XXXX-XXXX/Music /root/music
Replace XXXX-XXXX with your drive's actual ID.

5. Install Navidrome
Download and install Navidrome:

bash
Copy
Edit
cd /root
wget https://github.com/navidrome/navidrome/releases/latest/download/navidrome-linux-arm64.tar.gz
tar -xzf navidrome-linux-arm64.tar.gz
mv navidrome /opt/
Create a config file:

bash
Copy
Edit
mkdir /root/navidrome
nano /root/navidrome/navidrome.toml
Paste this into the file:

toml
Copy
Edit
MusicFolder = "/root/music"
Port = "4533"
Run Navidrome:

bash
Copy
Edit
/opt/navidrome/navidrome
6. Access Your Music Server
Open your phone's browser (or another device on the same network)

Go to: http://<your_phone_ip>:4533

Login with default creds: admin / admin

Change the admin password immediately from the UI.

7. Install Ultrasonic on Your Phone
Install Ultrasonic from F-Droid or GitHub

Connect it to your Navidrome instance using your phone’s local IP and port 4533

🧼 Bonus: My Setup
For aesthetics and practicality:

A simple phone stand keeps everything tidy and gives it that homelab feel ✨

🚀 What's Next?
This was my first step into the world of homelabbing. Next, I plan to:

Explore VPN setups for remote access

Try adding AdGuard Home for network-wide ad-blocking

Expand into other self-hosted services (e.g., file sharing, note-taking, etc.)

🧠 Why Do This?
Repurpose old hardware

Learn Linux, networking, and self-hosting

Own your data and your services

Just for fun 😄

