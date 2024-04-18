## Introduction

The Packet Ripper Proxy feature intercepts various network functions, allowing you to analyze and modify network packets in real-time. Whether you're testing the security of network applications or debugging network issues, the Packet Ripper Proxy provides the flexibility and control you need.

## Understanding Socket Types and Winsock Versions

### Socket Types

Sockets in network programming can be categorized into two main types: connected and unconnected. 

- **Connected Sockets**: These sockets are used in connection-oriented protocols, such as TCP. They establish a connection with another socket before transmitting data.

- **Unconnected Sockets**: These sockets are used in connectionless protocols, such as UDP. They do not establish a connection before transmitting data and can send data to multiple destinations without establishing a connection.

### Major Differences between Winsock and Winsock2 Functions

Winsock (Windows Sockets 1.1) and Winsock2 (Windows Sockets 2.0) are both API specifications for network programming in Windows. While they share many similarities, there are some significant differences:

- **Protocol Support**: Winsock2 supports additional protocols and features compared to Winsock, including multicast, quality of service (QoS), and overlapped I/O.

- **Socket Handling**: Winsock2 introduces a more robust socket handling model, including support for event-driven programming with overlapped I/O.

- **Namespace**: Winsock2 introduces a separate namespace (`WSA`) for its functions and data types to avoid conflicts with other Windows APIs.

For more detailed information about the differences between Winsock and Winsock2, refer to the [Windows documentation](https://docs.microsoft.com/en-us/windows/win32/winsock/about-windows-sockets-2).

## Proxy Functions

### Sending Functions

The sending functions, such as `send` and `sendto`, are commonly used in TCP and UDP communication, respectively. While `send` is used on a connected socket, `sendto` allows sending data to a specific destination, making it suitable for both connected and unconnected sockets.

- **Arguments (send):**
  - `s`: A descriptor identifying a connected socket.
  - `buf`: A pointer to the buffer containing the data to be transmitted.
  - `len`: The length, in bytes, of the data in the buffer.
  - `flags`: A set of flags that specify the way in which the call is made.

- **Arguments (sendto):**
  - `s`: A descriptor identifying a socket.
  - `buf`: A pointer to the buffer containing the data to be transmitted.
  - `len`: The length, in bytes, of the data in the buffer.
  - `flags`: A set of flags that specify the way in which the call is made.
  - `to`: A pointer to the address of the target socket.
  - `tolen`: The size, in bytes, of the `to` buffer.

For more information, refer to the [Windows documentation for `send`](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-send) and [sendto](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-sendto).

### Asynchronous Functions

The asynchronous functions, such as `WSASend` and `WSASendTo`, provide extended options for buffer management and notification callbacks. These functions are commonly used in scenarios where non-blocking operations are required, allowing for efficient handling of network communication.

- **Arguments (WSASend):**
  - `s`: A descriptor identifying a connected socket.
  - `lpBuffers`: A pointer to an array of `WSABUF` structures.
  - `dwBufferCount`: The number of buffers in the array.
  - `lpNumberOfBytesSent`: A pointer to the number of bytes sent by this call.
  - `dwFlags`: A set of flags that modify the behavior of the function call.
  - `lpOverlapped`: A pointer to a `WSAOVERLAPPED` structure.

- **Arguments (WSASendTo):**
  - `s`: A descriptor identifying a socket.
  - `lpBuffers`: A pointer to an array of `WSABUF` structures.
  - `dwBufferCount`: The number of buffers in the array.
  - `lpNumberOfBytesSent`: A pointer to the number of bytes sent by this call.
  - `dwFlags`: A set of flags that modify the behavior of the function call.
  - `lpTo`: A pointer to the address of the target socket.
  - `iTolen`: The size, in bytes, of the `lpTo` buffer.
  - `lpOverlapped`: A pointer to a `WSAOVERLAPPED` structure.

For more information, refer to the [Windows documentation for `WSASend`](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-wsasend) and [WSASendTo](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-wsasendto).

### Receiving Functions

The receiving functions, such as `recv` and `recvfrom`, are commonly used in TCP and UDP communication, respectively. While `recv` receives data from a connected socket, `recvfrom` receives data from a socket and retrieves the address of the sender.

- **Arguments (recv):**
  - `s`: A descriptor identifying a connected socket.
  - `buf`: A pointer to the buffer to receive the incoming data.
  - `len`: The length, in bytes, of the buffer.
  - `flags`: A set of flags that specify the way in which the call is made.

- **Arguments (recvfrom):**
  - `s`: A descriptor identifying a socket.
  - `buf`: A pointer to the buffer to receive the incoming data.
  - `len`: The length, in bytes, of the buffer.
  - `flags`: A set of flags that specify the way in which the call is made.
  - `from`: An optional pointer to a `SOCKADDR` structure that receives the address of the sender.
  - `fromlen`: An optional pointer to the size, in bytes, of the `from` buffer.

For more information, refer to the [Windows documentation for `recv`](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-recv) and [recvfrom](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-recvfrom).

### Asynchronous Receiving Functions

The asynchronous receiving functions, such as `WSARecv` and `WSARecvFrom`, offer advanced buffer management and notification options. These functions are commonly used in scenarios where non-blocking operations are required for efficient handling of incoming data.

- **Arguments (WSARecv):**
  - `s`: A descriptor identifying a connected socket.
  - `lpBuffers`: A pointer to an array of `WSABUF` structures.
  - `dwBufferCount`: The number of buffers in the array.
  - `lpNumberOfBytesRecvd`: A pointer to the number of bytes received by this call.
  - `lpFlags`: A pointer to flags that provide additional information about the receive operation.
  - `lpOverlapped`: A pointer to a `WSAOVERLAPPED` structure.

- **Arguments (WSARecvFrom):**
  - `s`: A descriptor identifying a socket.
  - `lpBuffers`: A pointer to an array of `WSABUF` structures.
  - `dwBufferCount`: The number of buffers in the array.
  - `lpNumberOfBytesRecvd`: A pointer to the number of bytes received by this call.
  - `lpFlags`: A pointer to flags that provide additional information about the receive operation.
  - `lpFrom`: An optional pointer to a `SOCKADDR` structure that receives the address of the sender.
  - `lpFromLen`: An optional pointer to the size, in bytes, of the `lpFrom` buffer.

For more information, refer to the [Windows documentation for `WSARecv`](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-wsarecv) and [WSARecvFrom](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-wsarecvfrom).

## Usage

To use the Packet Ripper Proxy feature, simply enable it in the Packet Ripper interface. Once enabled, the proxy will intercept network traffic according to the specified filters and rules.

### Packet Parsing

Additionally, you can utilize the parser feature in Packet Ripper to create custom rules for parsing specific types of packets intercepted by the proxy. This allows you to extract relevant information from the intercepted packets and perform actions based on the parsed data. For detailed instructions on configuring packet parsing rules, refer to the [parsers section](/user-guide/parsers) or the [python api section](api/parsers).

## Configuration

You can configure the Packet Ripper Proxy settings to define which network functions to intercept and how to handle intercepted packets. Refer to the Packet Ripper documentation for detailed configuration instructions.
