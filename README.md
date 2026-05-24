# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm
1.Start the program.
2.Get the frame size from the user
3.To create the frame based on the user request.
4.To send frames to server from the client side.
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
6.Stop the program
## Program 
Server.py
~~~
import socket
s = socket.socket()
s.bind(("localhost",8080))
s.listen(1)
print("Server running...")
while True:
    c,addr = s.accept()  
    request = c.recv(1024).decode()
    print("Request received")
    if "GET" in request:
        f = open("index.html","r")
        data = f.read()
        f.close()
        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())
    elif "POST" in request:
        data = request.split("\n\n")[1]
        f = open("upload.txt","w")
        f.write(data)
        f.close()
        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())
    c.close()
~~~
client.py
~~~
import socket
s = socket.socket()
s.connect(("localhost",8080))
ch = input("1.Download 2.Upload : ")
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())
    data = s.recv(4096)
    print(data.decode())
else:
    msg = input("Enter data to upload: ")
    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())
    data = s.recv(1024)
    print(data.decode())
s.close()
~~~

## OUTPUT
<img width="1920" height="1080" alt="Screenshot (247)" src="https://github.com/user-attachments/assets/f4712bf2-93c5-4163-b6be-5ec130e0a502" />
<img width="1920" height="1080" alt="Screenshot (246)" src="https://github.com/user-attachments/assets/f3a56865-9d93-4901-836b-056b77b1341b" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
