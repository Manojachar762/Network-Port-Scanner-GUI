# ui/Network-Port-Scanner-GUI

import threading
import socket
import tkinter as tk

# ---------------------- Scan Function ----------------------
def scan_ports():
    ip = entry_ip.get()

    # Clear previous output
    text_output.delete(1.0, tk.END)
    text_output.insert(tk.END, f"Scanning IP: {ip}\n")

    # Common ports list
    ports = [21, 22, 23, 25, 53, 80, 110, 139]

    for port in ports:
        try:
            # Create socket
            s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            s.settimeout(0.5)

            # Check port
            result = s.connect_ex((ip, port))

            if result == 0:
                text_output.insert(tk.END, f"Port {port} is OPEN\n")
            else:
                text_output.insert(tk.END, f"Port {port} is CLOSED\n")

            s.close()

        except Exception as e:
            text_output.insert(tk.END, f"Error on port {port}: {e}\n")