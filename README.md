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
## Server
```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server waiting for client...")
c, addr = s.accept()
size = int(input("Enter number of frames to send: "))
l = list(range(size))
ws = int(input("Enter Window Size: "))
st = 0
i = 0
while i < len(l):
    st = i + ws
    print("Sending frames:", l[i:st])
    c.send(str(l[i:st]).encode())
    ack = c.recv(1024).decode()
    if ack:
        print(ack)
        i += ws
    else:
        break
c.close()
s.close()
```
## Client
```
import socket
s = socket.socket()
s.connect(('localhost', 8000))
while True:
    data = s.recv(1024).decode()
    if data:
        print("Received frames:", data)
        s.send("ACK: Frames received".encode())
    else:
        break
s.close()
```
## OUTPUT

<img width="732" height="269" alt="image" src="https://github.com/user-attachments/assets/74694f78-9f45-4f90-8333-2c5d001ea28f" />

<img width="694" height="204" alt="image" src="https://github.com/user-attachments/assets/b7f2c4d0-b05e-4543-91c1-a52430e94721" />

## RESULT

Thus, python program to perform stop and wait protocol was successfully executed
