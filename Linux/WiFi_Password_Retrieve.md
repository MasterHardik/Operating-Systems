# WiFi Password Retrieval

## Table of Contents
1. [How to Retrieve Wi-Fi Password Using Terminal](#how-to-retrieve-wi-fi-password-using-terminal)
2. [Additional Information](#additional-information)

---

## How to Retrieve Wi-Fi Password Using Terminal

If you need to find the password for a Wi-Fi network using the terminal, follow these steps:

1. **Navigate to the NetworkManager Connections Directory**

   Open your terminal and run the following command to change to the directory where NetworkManager stores connection profiles:
   ```bash
   cd /etc/NetworkManager/system-connections/
    ```
2. **List Available Connections**

    To see a list of available network connection profiles, use the `ls` command:

    ```bash
    ls -a
    ```
    This will show you files representing your network connections. For example, you might see:

    ```bash
    HomeNetwork
    OfficeNetwork
    GuestNetwork
    ```
Identify the file corresponding to the Wi-Fi network for which you need the password. Suppose you want to find the password for `HomeNetwork`.

3. **View the Connection File**

    Open the connection file using the `cat` command to view its contents:

    ```bash
    sudo cat "HomeNetwork"
    ```
    The output might look like this:

    ```makefile
    [connection]
    id=HomeNetwork
    uuid=12345678-1234-1234-1234-123456789abc
    type=wifi
    autoconnect=true

    [wifi]
    ssid=HomeNetwork
    mode=infrastructure

    [wifi-security]
    key-mgmt=wpa-psk
    psk=SuperSecretPassword123

    [ipv4]
    method=auto
    ```
4. **Find the Wi-Fi Password**

    In the file, look for the line starting with psk=. In this example, it is:
    ```makefile
    psk=SuperSecretPassword123
    ```

    This is the Wi-Fi password. Make sure to copy it securely.

5. **Close the File**

    If you used `cat`, you can simply exit the terminal. If you used a text editor, ensure to save any changes and close the editor properly.


## Additional Information

- Permissions: Accessing the connection files requires root permissions. You will need to use sudo to view or edit these files.

- Security: Be cautious when handling and sharing Wi-Fi passwords to avoid unauthorized access to your network.

- Different Systems: This method works for systems using NetworkManager, which is common in many Linux distributions. For other network management systems, the procedure may vary.


Feel free to ask if you have any more questions or need further assistance!

***Note**: The following instructions are provided for educational purposes only. Ensure you have proper authorization before accessing or retrieving network credentials.*