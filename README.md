## REG.NO:212224110035

# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM

client

```
import socket

s = socket.socket()
host = socket.gethostname()
port = 60002
print(f"Connecting to server {host}:{port}...")
s.connect((host, port))
s.send("Hello server!".encode())

with open('received_file.txt', 'wb') as f:
    while True:
        data = s.recv(1024)
        if not data:
            break
        f.write(data)

print('Successfully received the file.')
s.close()
print('Connection closed.')
```
server
```
import socket

port = 60002
s = socket.socket()
host = socket.gethostname()
s.bind((host, port))
s.listen(5)

print(f"Server is listening on {host}:{port}...")

while True:
    conn, addr = s.accept()
    print(f"Connected by {addr}")

    data = conn.recv(1024)
    print('Server received:', repr(data))

    filename = 'mytext.txt'
    with open(filename, 'rb') as f:
        l = f.read(1024)
        while l:
            conn.send(l)
            print('Sent', repr(l))
            l = f.read(1024)

    print('File sent successfully!')
    conn.close()
    print('Connection closed.\n')
```
## OUPUT
<img width="714" height="243" alt="cn 3c" src="https://github.com/user-attachments/assets/090f9e6b-8dcc-4031-a220-dad398eb2a85" />

<img width="747" height="205" alt="cn 3c(1)" src="https://github.com/user-attachments/assets/99c08854-6c14-4e53-92d4-23968ec16a32" />

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
