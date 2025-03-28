# File Transfer Methods

This repository contains various methods and commands for transferring files between different systems, including Linux, Windows, and over different protocols like HTTP, FTP, SSH, SMB, WinRM, and more.

## Usage

Each directory contains instructions for transferring files using different methods:

### Linux File Transfer

- **local-to-remote**: Instructions for transferring files from a local Linux system to a remote system.
- **remote-to-local**: Instructions for transferring files from a remote Linux system to a local system.

### Windows File Transfer

- **local-to-remote**: Instructions for transferring files from a local Windows system to a remote system.
- **remote-to-local**: Instructions for transferring files from a remote Windows system to a local system.

## Methods Covered

The methods covered in this repository include:

- Using `wget` and `curl` for HTTP(S) transfers.
- Using PowerShell for web content download and upload.
- Using `certutil` for web content download and decoding.
- Setting up and using SMB servers and clients for file transfer.
- Using SSH for SCP and RSYNC file transfers.
- Using WinRM for file transfer on Windows systems.
- Using BITSADMIN for file transfer.
- Using NC (Netcat) for file transfer.
- Using FTP for file transfer.

## How to Use

Each method includes detailed commands and examples for both downloading and uploading files. Simply follow the instructions provided in the respective `README.md` files within each directory for the desired transfer method.

## Note

Ensure that you have the necessary permissions and access rights before attempting file transfers, especially when using authentication methods like SMB, SSH, or FTP.
