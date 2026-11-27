# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## NAME: VISHAL R
## REG NO: 212225230307
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM
client:
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

filename = input("Enter the filename: ")

s.send(filename.encode())

with open(filename, "rb") as f:
    while True:
        data = f.read(1024)
        if not data:
            break
        s.sendall(data)

s.shutdown(socket.SHUT_WR)

ack = s.recv(1024).decode()
print("Server:", ack)

s.close()
```

server:
```
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)

print("Server is waiting for connection...")

c, addr = s.accept()
print("Connected to:", addr)

filename = c.recv(1024).decode()

with open("received_" + filename, "wb") as f:
    while True:
        data = c.recv(1024)
        if not data:
            break
        f.write(data)

print("File received successfully")

c.send("File received successfully".encode())

c.close()
s.close()
```

## OUPUT
client:

<img width="1917" height="1040" alt="Screenshot 2026-11-27 082036" src="https://github.com/user-attachments/assets/b46b1f02-8df0-4efa-8c48-b61c1b070f16" />

server:

<img width="1917" height="1037" alt="Screenshot 2026-11-27 082129" src="https://github.com/user-attachments/assets/27100a04-9a8e-4605-8f0c-7a6ee0fa332b" />


## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
