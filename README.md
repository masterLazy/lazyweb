# LazyWeb
A new **HTTP** SDK strives to be perfect and easy to use. (I have developed mWeb but I thought it was trash so I decide to create this. ) Both **HTTP Client** and **HTTP Server** are supported in LazyWeb.

## Introduction
LazyWeb is based on Windows API (WinSock) and OpenSSL and multi-threaded.

LazyWeb offers a class, `lazy::Web`, as the interface. It could be used to `connect()`, `write()`, `read()` for **Client** use. The I/O is also suppored SSL. Also, `lazy::Web` offers `write()`, `read()`, `listen()`, `accept()` for **Server** use. LazyWeb creates a `recv_thread` to receive messages so that LazyWeb will be **non-blocking**. All the messages will be stored to a file at once.

LazyWeb uses class `lazy::Msg` to manage http messages, and offers `lazy::WebHelper` to help `lazy::Web` and developers work.

## Quickstart

### Start as Client

```cpp
#include <iostream>
using namespace std;
//Includes the lib
#include <lazyweb/lazyweb.hpp>
using namespace lazy;
int main()
{
  string url="https://www.microsoft.com/en-us/"

  //Instantiate lazy::web
  Web web;
  //Initializate
  web.init();
  //Connect to the server
  web.connect(url);

  //Send a GET msg
  WebHelper(web).send_get_msg(url);

  //Wait and recv msg
  while(web.msg_empty());
  Msg msg = web.read();
  //Print the msg
  cout << msg.get_str() << endl;

  //Close
  web.close();
  return 0;
}
```

## #include<> tree
`lazyweb.hpp`
|- `httpMsg.hpp`
|- `webHelper.hpp`
|- `main.hpp`

## Situation
The development of LazyWeb is nearly half-done. It's under development. mLazy drew this picture to show his basic ideas:

![basic idea](basic_idea.png)
