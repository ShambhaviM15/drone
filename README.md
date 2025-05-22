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
