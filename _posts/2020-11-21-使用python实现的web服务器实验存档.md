---
layout:     post
title:      "使用python实现的多线程web服务器"
subtitle:   ""
date:       2020-11-21 17:00:00
author:     "xnchen"
header-img: "img/home-bg.jpg"
tags:
    - 计算机网络
    - python
    - socket
---

test post
![](/asset/.2020-11-21-使用python实现的web服务器实验存档_images/166f1748.png)

    {% highlight ruby %}
    #import socket module
    from socket import *
    import threading
    import re
    import os
    {% endhighlight %}
    
test 2

    def server_enter(address='', port=12000):
        server_socket = socket(AF_INET, SOCK_STREAM)
        server_socket.bind((address, port))
        server_socket.listen(10)
    
        while(1):
            connection_socket, addr = server_socket.accept()
            sub_thread = threading.Thread(target = handle_client, args=(connection_socket, addr))
            sub_thread.start()
    
    def find_target_file_path(request_row):
        file_name = ""
        url_pattern = r"[^/]+(/[^ ]*)"
        match_object = re.match(url_pattern, request_row)
        if match_object:
            file_name = match_object.group(1)
            if file_name == "/":
                file_name = "/index.html"
        return file_name[1:]
    
    def handle_client(socket, addr):
    
        recv_data = socket.recv(1024).decode("utf-8")
        request_header_lines = recv_data.splitlines()
        response = ""
        '''
        for line in request_header_lines:
            print(line)
        '''
        
        file_name = find_target_file_path(request_header_lines[0])
        # print(os.path.join('.', 'src', file_name))
        try:
            src_file = open(os.path.join('.', 'src', file_name), 'rb')
            response = "HTTP/1.1 200 OK\r\n"
            response += "\r\n"
        except IOError:
            src_file = open(os.path.join('.', 'src', '404notfound.html'), 'rb')
            response = "HTTP/1.1 404 Not Found\r\n"
            response += "\r\n"
        finally:
            html_content = src_file.read()
            src_file.close()
        
    
        socket.send(response.encode("utf-8"))
        socket.send(html_content)
    
        socket.close()
    
    if __name__ == "__main__":
        server_enter()
            

