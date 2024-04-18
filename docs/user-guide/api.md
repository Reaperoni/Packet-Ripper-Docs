# Python Encryption/Decryption API Documentation

Welcome to the Python Encryption/Decryption API Documentation for Packet Ripper! This documentation provides detailed information on how to use the Python API for encryption and decryption in Packet Ripper.

## Overview


The Python Encryption/Decryption API allows users to customize the encryption and decryption process for intercepted network packets in Packet Ripper. By providing a Python script with encryption and decryption functions, users can integrate their own encryption algorithms or techniques into the Packet Ripper proxy in real-time.

  

### Key Components

  

-  **Encryption/Decryption Script**: A Python script containing encryption and decryption functions.

-  **Settings Configuration**: Configuration settings within Packet Ripper to specify the path to the Python script and the names of the encryption and decryption functions.

-  **Integration with Packet Ripper**: The Python API seamlessly integrates with the Packet Ripper proxy, enabling on-the-fly encryption and decryption of intercepted network packets.

  

## Usage

  

To utilize the Python Encryption/Decryption API in Packet Ripper, follow these steps:

  

1.  **Create Encryption/Decryption Script**: Write a Python script containing encryption and decryption functions. By default, the script is named `encryptionDecryption.py` and resides in the Packet Ripper settings directory.

  

2.  **Configure Settings**: In the Packet Ripper settings, specify the path to the Python script and the names of the encryption and decryption functions.

  

3.  **Integration with Proxy**: Packet Ripper automatically calls the specified encryption or decryption function from the Python script, passing the intercepted network packet data as input.

  

4.  **Customize Encryption/Decryption**: Customize the encryption and decryption process in the Python script according to your security requirements and algorithms.

  

### Example Encryption/Decryption Script

  

``` py 
    def encryptBuffers(buffers): # Encrypts buffers with xor, this function is called when resending packets
      encrypted = []
      for hex_string in buffers:
        bytes_data = bytes.fromhex(hex_string)
        encrypted_bytes = bytearray([b ^  0xFF  for b in bytes_data])
        encrypted.append(encrypted_bytes.hex())
      return buffers


    def decrypt(buffers): # Simple XOR decryption function with parsing. Called When a packet is added to the proxy before the built in parser
      decrypted_list = []
      for hex_string in buffers:
        bytes_data = bytes.fromhex(hex_string)
        decrypted_bytes = bytearray([b ^  0xFF  for b in bytes_data])
        decrypted_list.append(decrypted_bytes.hex())\
      for i in decrypted_list:
        i = parse(decrypted_list)
      return decrypted_list

    def  parseShootPacket(buffer): # Parsing shoot Packet
      return  "Shoot packet" # this is what shows in the the proxy now instead of the og buffer


    def parseMovePacket(buffer):
      buffer = buffer[4:]
      x = float.fromhex(buffer[:8])
      y = float.fromhex(buffer[8:16])
      z = float.fromhex(buffer[16:24])
      pitch = int.fromhex(buffer[24:26])
      yaw = int.fromhex(buffer[26:28])
      roll = int.fromhex(buffer[28:30])
      parsed =  "Move packet: x: "  + str(x) +  " y: "  + str(y) +  " z: "  + str(z)
      parsed +=  " pitch: "  + str(pitch) +  " yaw: "  + str(yaw) +  " roll: "  + str(roll)
      return parsed


  def parse(buffer): #decides what type of packet it is by opcode and calls corresponding parsing function
      prefix = buffer[:4]
      if prefix ==  "6D76":
      return parseMovePacket(buffer)
      elif prefix ==  "2A69":
      return parseShootPacket(buffer)
      return buffer
```