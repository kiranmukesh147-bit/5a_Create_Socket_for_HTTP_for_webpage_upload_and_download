# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## Program 
CLIENT
```
import socket
s = socket.socket()
s.connect(("localhost", 1234))
request = "GET / HTTP/1.1\r\nHost: localhost\r\n\r\n"
s.sendall(request.encode())
data = b""
while True:
    part = s.recv(4096)
    if not part:
        break
    data += part
# Remove HTTP headers
webpage = data.split(b"\r\n\r\n", 1)[1]
with open("download.html", "wb") as f:
    f.write(webpage)
print("Webpage downloaded successfully!")
print("Saved as download.html")
s.close()
```
SERVER
```

import socket

s = socket.socket()
s.bind(("localhost", 1234))

s.listen(1)
print("Server is waiting for client...")

conn, addr = s.accept()
print("Client connected:", addr)

request = conn.recv(1024).decode()
print("Request:", request)

with open("index.html", "rb") as f:
    webpage = f.read()

response = (
    b"HTTP/1.1 200 OK\r\n"
    b"Content-Type: text/html\r\n"
    b"Content-Length: " + str(len(webpage)).encode() +
    b"\r\nConnection: close\r\n\r\n" + webpage
)

conn.sendall(response)

print("Webpage sent successfully!")
conn.close()
s.close()
```
INDEX.HTML
```
<html>
<head>
    <title>My Webpage</title>
</head>
<body>
    <h1>Welcome</h1>
    <p>HTTP Socket Programming</p>
</body>
</html>
```
## OUTPUT

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ff9df2f5-0672-4e24-bd07-85ac09ddfd33" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/bfaf4c8e-29c3-4089-b34b-ff53a2680d7b" />


## Result
Thus the socket for HTTP for web page upload and download created and Executed
