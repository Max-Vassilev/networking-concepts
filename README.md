# networking-journey

Repo for mastering networking basics and enabling external access to a web app.

# Networking Concepts and Setup

This document provides an overview of the key networking concepts and how to set up a Django project to be accessed within a local network and externally through port forwarding.

## TCP/IP Model

The **TCP/IP model** governs how data travels across the internet. It has four layers, each handling a different part of the communication process:

1. **Application Layer**: User-facing services like HTTP, FTP, and DNS.
2. **Transport Layer**: Ensures reliable data delivery using TCP or UDP.
3. **Internet Layer**: Handles IP addressing and routing.
4. **Network Access Layer**: Manages physical data transmission (e.g., Ethernet, Wi-Fi).

## DNS

The **Domain Name System (DNS)** translates a human-readable domain name (like `example.com`) into an IP address (e.g., `93.184.216.34`). When you type a URL in your browser, the DNS server looks up the domain and returns the corresponding IP address. Your browser then connects to that IP to load the website.

## TLS

**TLS (Transport Layer Security)** is a protocol that encrypts data exchanged between your browser and the server to ensure secure communication. It prevents anyone from intercepting or tampering with the data while it's being transferred.

When a website uses HTTPS, it means the connection is secured using TLS. This is different from HTTP, which is insecure.

## SSL

**SSL (Secure Sockets Layer)** is the older version of TLS. While both SSL and TLS serve the same purpose of securing communications, SSL is less secure, and TLS is the more modern, stronger protocol.

## NAT (Network Address Translation)

**NAT** allows multiple devices within a private network to share a single public IP address when accessing the internet. It modifies the IP address in packet headers to ensure proper routing between private networks and the internet.

## Networking Setup in a Home Network

In a typical home network, each device (like laptops, phones, etc.) is assigned a unique local IP address by the router. These addresses typically fall within the range `192.168.x.x`.

### Example Setup

- **Laptop 1** (running a Django project) has the IP address `192.168.1.2`.
- **Laptop 2** wants to access the Django project running on Laptop 1.

### Communication Between Laptops

1. **Laptop 1** runs the Django project on `0.0.0.0:8000` to make it accessible to other devices on the network (instead of just `127.0.0.1`, which is only accessible locally on Laptop 1).
2. **Laptop 2** can access the Django project by visiting `http://192.168.1.2:8000` in its browser, which points to the Django server on Laptop 1.

### Key Points

- `192.168.x.x` IPs are local network addresses.
- Devices within the same network (like Laptop 1 and Laptop 2) can communicate with each other.
- The `0.0.0.0` binding allows Laptop 1’s Django project to be accessible by other devices in the local network.

## Port Forwarding for External Access

To make a web application accessible externally (from outside the local network), you need to set up **port forwarding** on your router. This allows external traffic to reach a specific device within your local network.

### Example Setup:

```plaintext
           Internet
                 |
     http://32.14.217.46:8000  <— Outer IP Address of the router
                 |
           [Router]
         Private IP: 192.168.1.1   <— Inner IP Address of the router
                |
            Laptop
         192.168.1.2
       (Django server)
```
