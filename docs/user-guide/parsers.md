# Parser Documentation

Welcome to the Packet Ripper Parser documentation! The parser feature in Packet Ripper allows you to create custom rules for parsing specific types of packets intercepted by the proxy. This enables you to extract relevant information from intercepted packets and perform actions based on the parsed data.

## Introduction

In network communication, packets often use opcodes to distinguish themselves and indicate the type of data they contain. For example, in a game network protocol, packets may have opcodes that represent different types of game events or data structures.

For instance, consider a game where player positions are transmitted as packets. Each player position packet may have an opcode of 2576, and the next 12 bytes could represent the player's X, Y, and Z coordinates, each taking up 4 bytes.

The parser in Packet Ripper leverages these opcodes to identify the type of data contained in intercepted packets and converts the hexadecimal representation into the desired data type with the specified size.

## Parsing and Packet Reconstruction

Once intercepted packets are parsed by the Packet Ripper parser, the parsed data can be displayed in a variety of formats, including a hex editor. This allows you to reconstruct packets visually and manipulate them as needed.

For example, after parsing a player position packet with opcode 2576, the parser would extract the X, Y, and Z coordinates from the packet's hexadecimal representation. You can then view and modify these coordinates in the [Hex-Editor](/user-guide/hex-editor), allowing you to adjust the player's position resend it to the game.

## Enhanced Packet Analysis

In addition to packet reconstruction, the parser in Packet Ripper enables enhanced packet analysis by providing insights into the structure and content of intercepted packets. By defining parsing rules for specific packet types, you can extract meaningful information such as player actions, game events, or network protocol details.

For instance, you could create parsing rules to identify and extract chat messages from game packets, allowing you to monitor in-game communication or detect suspicious activity.

## Using the Parser

To use the parser feature, follow these steps:

1. **Define Parsing Rules**: Create custom parsing rules specifying the packet opcodes and the desired data types and sizes.
   
2. **Intercept Packets**: Enable the Packet Ripper Proxy to intercept network traffic and capture packets that match the defined parsing rules.
   
3. **Parse Intercepted Packets**: The parser will automatically process intercepted packets according to the defined parsing rules, converting hexadecimal data into the specified data types.

4. **View Parsed Data**: The parsed data will be displayed visually within the Packet Ripper interface, including the hex editor, allowing you to inspect and manipulate the packet contents as needed.

## Configuration

You can configure parsing rules in Packet Ripper by accessing the parser settings. Here, you can define the packet opcodes, specify the data types and sizes for parsing, and manage parsing rules. The enable option simply dictates wether the proxy will parse that specific data parser, however this will still show in the Hex-Editor when we want to resend. The ignore option makes it so the proxy ignores that specific type of packet that matches that opcode. This is particular useful when you only want to see packets you haven't discovered yet.

## Example

Here's an example of how to create a parsing rule in Packet Ripper:

1. **Define Rule**: Specify the packet opcode to target and the data type and size for parsing (e.g., opcode `2576` represents player position data with X, Y, and Z coordinates each occupying 4 bytes)![Example Parser](/images/parser-example.png)Notice how even though each float should take 4 bytes we have 8. This is due to the fact 1 byte is represented by 2 hex digits. Even though this might be a bit confusing, its necessary for the freedom when resending or parsing packets with uneven sizes.

2. **Intercept Packets**: Enable the Packet Ripper Proxy to intercept packets containing the specified opcode.

3. **Parse Intercepted Packets**: The parser will convert the hexadecimal data corresponding to the specified opcode into the desired data type with the specified size.

4. **View Parsed Data**: The parsed data will be displayed within the Packet Ripper interface, including the hex editor, allowing you to view and interact with the parsed packet contents.

## Conclusion

The parser feature in Packet Ripper provides powerful capabilities for analyzing and manipulating intercepted network packets. By defining custom parsing rules, you can extract valuable information from packet data and gain deeper insights into network communication.

For detailed instructions on configuring parsing rules with the python api see [here](/api/parsers)
