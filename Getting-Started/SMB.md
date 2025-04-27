# SMB (Server Message Block) – Accessing Shares

**SMB (Server Message Block)** is a network file sharing protocol used for providing access to shared files, printers, and other resources across a network.

---

### Question Statement

- **Objective**: Identify and enumerate the SMB shares on the target system. Once you've located the shares, authenticate as the **bob** user and navigate to the **flag** folder. Inside, you’ll find the **flag.txt** file. Your mission is to extract its contents and retrieve the flag.

In this challenge, we had to exploit SMB shares, gain access as the **bob** user, and extract the flag hidden within the **flag.txt** file. Time to hack into the system and retrieve our prize!


---

### Steps I Followed:

- **Step 1**: Use Nmap to scan for SMB shares on the target host.

    ```bash
    nmap --script smb-enum-shares <IP-ADDRESS>
    ```
    - This command runs an Nmap scan using the `smb-enum-shares` script to enumerate SMB shares on the target IP.
    - _Snapshot of the result:_
    ![Nmap SMB Scan](path/to/snapshot)

- **Step 2**: Connect to the SMB share as the **bob** user.

    ```bash
    smbclient -U bob \\\\10.129.74.154\\users
    ```
    - The **`smbclient`** command connects to SMB shares, and by default, it uses **port 445** for the connection if no port is explicitly specified. This is the standard port for SMB communication, so even though we didn't specify a port in the command, **`smbclient`** automatically attempted to connect via port 445.

    - _Snapshot of the result:_
    ![Connection Attempt](path/to/snapshot)

- **Step 3**: Once logged in, list the available directories in the share.

    ```bash
    smb: \> ls
    ```
    - This lists the files and directories in the **users** share, where we find the **flag** directory.
    - _Snapshot of the result:_
    ![Directory Listing](path/to/snapshot)

- **Step 4**: Navigate into the **flag** directory and list its contents.

    ```bash
   smb: \> cd flag
   smb: \flag\> ls
    ```
    - The first command changes the current directory to flag, where we expect to find **flag.txt**. The second command **lists** the contents of the flag directory, showing the flag.txt file.

    - _Snapshot of the result:_
    ![Change Directory](path/to/snapshot)

- **Step 5**: Retrieve the **flag.txt** file from the share.

    ```bash
    smb: \flag\> get flag.txt
    ```
    - This command downloads the **flag.txt** file from the share to the local machine.
    - _Snapshot of the result:_
    ![File Download](path/to/snapshot)

---

### Final Outcome

The **flag.txt** file was successfully retrieved and stored in the local folder.

---

