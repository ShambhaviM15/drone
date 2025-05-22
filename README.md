from fpdf import FPDF

# Create PDF document
class PDF(FPDF):
    def header(self):
        self.set_font("Arial", "B", 14)
        self.cell(0, 10, "Raspberry Pi OS: Command Guide & Beginner Projects", ln=True, align="C")
        self.ln(5)

    def section_title(self, title):
        self.set_font("Arial", "B", 12)
        self.set_text_color(30, 30, 120)
        self.cell(0, 10, title, ln=True)
        self.set_text_color(0, 0, 0)

    def section_body(self, body):
        self.set_font("Arial", "", 11)
        self.multi_cell(0, 8, body)
        self.ln()

pdf = PDF()
pdf.add_page()

# Introduction
pdf.section_title("Overview")
pdf.section_body(
    "Raspberry Pi OS is a Debian-based Linux operating system for Raspberry Pi. "
    "It supports both GUI and CLI operation modes. Below is a categorized list of over 60 essential terminal commands, "
    "followed by beginner-friendly project ideas to apply your knowledge."
)

# Command categories
commands = {
    "File & Directory Commands": [
        "ls - List files", "cd - Change directory", "pwd - Print working directory", "mkdir - Create directory",
        "rmdir - Remove directory", "touch - Create empty file", "cp - Copy files/directories",
        "mv - Move/rename files", "rm - Remove files/directories", "find - Search for files", "tree - Show directory tree",
        "stat - Show file metadata"
    ],
    "Package Management (APT)": [
        "sudo apt update - Update package lists", "sudo apt upgrade - Upgrade packages",
        "sudo apt install <pkg> - Install a package", "sudo apt remove <pkg> - Remove a package",
        "sudo apt autoremove - Remove unused packages", "sudo apt list --installed - List installed packages",
        "sudo apt search <pkg> - Search for a package"
    ],
    "System Information & Management": [
        "uname -a - Show system info", "hostname - Show hostname", "top - Real-time process monitor",
        "htop - Advanced system monitor", "free -h - Show memory usage", "df -h - Disk space usage",
        "du -sh * - Size of files/folders", "uptime - Show uptime", "whoami - Current user", "id - Show user info",
        "date - Show date/time"
    ],
    "User and Permissions": [
        "adduser <name> - Add user", "passwd <name> - Change password", "sudo - Run as root",
        "chmod +x file - Make file executable", "chown user:group file - Change ownership", "groups - Show user groups"
    ],
    "Networking": [
        "ping google.com - Test network", "ifconfig - Show interfaces", "ip a - Show IPs",
        "hostname -I - Show local IP", "curl <url> - Get content from URL", "wget <url> - Download from URL",
        "ssh pi@<ip> - Remote login", "scp file pi@<ip>:~/ - Copy file remotely"
    ],
    "Process & Service Management": [
        "ps aux - List processes", "kill <PID> - Kill process", "systemctl status - Check service",
        "systemctl start <svc> - Start service", "systemctl stop <svc> - Stop service",
        "systemctl restart <svc> - Restart service", "reboot - Reboot system", "shutdown now - Shutdown now"
    ],
    "Miscellaneous": [
        "raspi-config - Raspberry Pi config", "crontab -e - Edit cron jobs", "nano <file> - Edit file",
        "cat <file> - View file", "dmesg - Kernel messages", "journalctl - View logs", "clear - Clear terminal",
        "man <cmd> - Command manual"
    ]
}

for category, cmds in commands.items():
    pdf.section_title(category)
    pdf.section_body("\n".join(cmds))

# Projects section
pdf.section_title("Beginner Raspberry Pi Projects")
projects = [
    "1. File Server with Samba - Share files across your network.",
    "2. Web Server with Apache/Nginx - Host simple websites or apps.",
    "3. Pi-hole Ad Blocker - Block ads network-wide with one command.",
    "4. Temperature Monitor - Use sensors to log room temperature.",
    "5. Media Center - Turn Pi into a streaming hub with Kodi.",
    "6. Retro Gaming Console - Play retro games using RetroPie.",
    "7. Automated Backups - Schedule daily USB or network backups.",
    "8. Weather Station - Fetch weather data from APIs and display."
]
pdf.section_body("\n".join(projects))

# Save PDF
pdf_path = "/mnt/data/Raspberry_Pi_OS_Commands_and_Projects.pdf"
pdf.output(pdf_path)
pdf_path



pwd: Print current working directory.
Example: pwd → /home/pi
cd <directory>: Change to a directory.
Example: cd Documents
cd ..: Move up one directory.
cd ~: Go to home directory.
cd /: Go to root directory.
ls: List files and directories.
ls -l: Detailed list (permissions, size, etc.).
ls -a: Show hidden files.
ls -la: Detailed list including hidden files.
tree: Display directory structure (install with sudo apt install tree).
File and Directory Management
touch <filename>: Create an empty file.
Example: touch test.txt
mkdir <dirname>: Create a directory.
Example: mkdir myfolder
rm <filename>: Remove a file.
Example: rm test.txt
rm -r <dirname>: Remove a directory and its contents.
Example: rm -r myfolder
cp <source> <destination>: Copy a file.
Example: cp file.txt /home/pi/backup/
mv <source> <destination>: Move or rename a file/directory.
Example: mv file.txt newfile.txt
find <path> -name <filename>: Search for a file.
Example: find /home -name "*.txt"
ln -s <source> <linkname>: Create a symbolic link.
Example: ln -s /home/pi/file.txt link
cat <filename>: Display file contents.
Example: cat file.txt
less <filename>: View file contents with scrolling (press q to quit).
File Editing
nano <filename>: Open file in Nano editor.
Example: nano script.py
vim <filename>: Open file in Vim editor.
echo "text" > <filename>: Write text to a file (overwrites).
Example: echo "Hello" > file.txt
echo "text" >> <filename>: Append text to a file.
Example: echo "World" >> file.txt
File Inspection
head <filename>: Display first 10 lines of a file.
Example: head file.txt
tail <filename>: Display last 10 lines of a file.
wc <filename>: Count lines, words, characters in a file.
Example: wc file.txt
file <filename>: Show file type.
Example: file image.jpg
Permissions
chmod <permissions> <filename>: Change file permissions.
Example: chmod 755 script.sh
chown <user> <filename>: Change file owner.
Example: chown pi file.txt
ls -l: Check file permissions.
sudo: Run a command as superuser.
Example: sudo nano /etc/config
System Information
uname -a: Display system information.
df -h: Show disk space usage (human-readable).
free -h: Display memory usage.
top: Monitor running processes (press q to quit).
htop: Interactive process viewer (install with sudo apt install htop).
uptime: Show system uptime and load.
whoami: Display current user.
hostname: Show system hostname.
Package Management
sudo apt update: Update package lists.
sudo apt upgrade: Upgrade installed packages.
sudo apt install <package>: Install a package.
Example: sudo apt install vim
sudo apt remove <package>: Remove a package.
sudo apt autoremove: Remove unused dependencies.
Networking
ping <host>: Check connectivity to a host.
Example: ping google.com
ifconfig: Display network interfaces (or use ip addr).
wget <url>: Download a file from the web.
Example: wget http://example.com/file
curl <url>: Fetch data from a URL.
Example: curl http://example.com
System Control
sudo reboot: Restart the Raspberry Pi.
Example: sudo reboot
