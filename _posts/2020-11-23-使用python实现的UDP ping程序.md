---
layout:     post
title:      "使用python实现的UDP ping程序实验存档"
subtitle:   ""
date:       2020-11-23 16:40:00
author:     "xnchen"
header-img: "img/home-bg.jpg"
tags:
    - 计算机网络
    - python
    - socket
---

    # -*- coding: utf-8 -*-
    # @Author: xnchen
    # @Emmail: xnchen97@gmail.com
    # @Date:   2020-11-23 15:49:52
    # @Last Modified by:   xnchen
    # @Last Modified time: 2020-11-23 16:39:28
    
    from socket import *
    import threading
    from time import time, sleep
    
    # 参数
    server_name = "127.0.0.1"
    port = 12000
    ping_test_time = 10
    wait_time = 0
    success_cnt = 0
    
    # 这个是关键，设置新的socket对象的timeout时间，如果达到没有接收到就抛出一个socket.timeout异常类
    setdefaulttimeout(1)
    
    def handle_client(server_name, port):
        global wait_time, success_cnt
        message = "this is a test message."
    
    
        try:
            with socket(AF_INET, SOCK_DGRAM) as client_socket:
                start_time = time()
    
                client_socket.sendto(message.encode(), (server_name, port))
                modified_message, server_address = client_socket.recvfrom(2048)
    
                end_time = time()
    
                print("successful recv, mess: ", modified_message.decode())
                print("RTT: ", format(end_time-start_time, '0.7f'))
    
                wait_time += end_time-start_time
                success_cnt += 1
    
        except timeout:
            print("error! socket time out!")
        except Exception as e:
            print(e)
    
    
    def main():
    
        for i in range(ping_test_time):
            print(i)
            sub_thread = threading.Thread(target = handle_client, args = (server_name, port))
            sub_thread.start()
        
        sleep(2)
        print('=======> all UDP message end!, all success message: (', success_cnt,'/', ping_test_time, ')')
        if success_cnt>0:
            print('=======> average RTT: ', format(wait_time/success_cnt, '0.7f'))
        else:
            print('sucess cnt is 0, try again. ')
    
    if __name__ == '__main__':
        main()