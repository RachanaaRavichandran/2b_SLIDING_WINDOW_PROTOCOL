# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
client.py
```
import socket

# Create socket
client_socket = socket.socket()

# Bind and listen
client_socket.bind(('localhost', 8000))
client_socket.listen(1)

print("Waiting for receiver connection...")

# Accept connection
conn, addr = client_socket.accept()
print("Connected with:", addr)

# Input details
size = int(input("Enter number of frames to send: "))
window_size = int(input("Enter window size: "))

frames = list(range(size))

i = 0

while i < len(frames):

    # Select frames according to window size
    window = frames[i:i + window_size]

    # Send frames
    conn.send(str(window).encode())

    print("Sent Frames:", window)

    # Receive acknowledgement
    ack = conn.recv(1024).decode()

    print("Receiver:", ack)

    # Move to next window
    i += window_size

print("All frames sent successfully")

conn.close()
client_socket.close()
```
server.py
```
import socket

# Create socket
server_socket = socket.socket()

# Connect to sender
server_socket.connect(('localhost', 8000))

print("Connected to sender")

while True:

    # Receive frames
    data = server_socket.recv(1024).decode()

    # Stop if no data
    if not data:
        break

    print("Received Frames:", data)

    # Send acknowledgement
    server_socket.send("Acknowledgement received".encode())

server_socket.close()
developed by:R.Rachanaa
ref no: 212225040322
```
## OUPUT
client.py
<img width="376" height="320" alt="image" src="https://github.com/user-attachments/assets/1d77295c-1a0e-4b02-bd42-737b2864c638" />

server.py
<img width="412" height="176" alt="image" src="https://github.com/user-attachments/assets/ccd38fd0-cc24-47a5-9d2a-90d73617f5ea" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
