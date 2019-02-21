---
title: 对于 SAN 复制套接字处理
description: 对于 SAN 复制套接字处理
ms.assetid: d8e8cb6d-fcdb-4121-9a44-a2bc884ab620
keywords:
- Windows 套接字直接 WDK，套接字句柄
- SAN 套接字 WDK，复制套接字句柄
- WDK Windows 套接字直接挂起
- 复制套接字处理 WDK San
- 共享基础套接字 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bafb3c2242cbb22fe1508399400f1c7a6fe50f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526785"
---
# <a name="duplicating-socket-handles-for-a-san"></a>对于 SAN 复制套接字处理





在不同进程中运行的多个应用程序可以使用 Windows 套接字开关在共享基础套接字上执行操作。 但是，一次只有一个应用程序可以执行对该共享的基础套接字操作。

若要使用共享的基础套接字，应用程序必须通过以下方式之一来检索该基础套接字的重复句柄：

-   直接通过调用 Windows 套接字**WSADuplicateSocket**函数

    控制进程的上下文中进行调用 （在其中创建套接字的进程）。

-   间接方法，通过调用 Win32 DuplicateHandle 函数

    Noncontrolling 进程 （而不是过程中在其中创建套接字） 的上下文中进行调用。

-   使用句柄继承机制

    子进程 （noncontrolling 进程） 继承所有或部分在其父进程 （控制进程） 中创建的句柄。

-   在正常连接闭包

    如果某些数据仍保持发送时，控制进程中的应用程序关闭套接字并退出，此剩余的数据进行缓冲处理 Windows 套接字 DLL 中。 系统服务进程 （noncontrolling 进程） 的上下文中的另一个应用程序随后会发送此数据。

Windows 套接字开关，结合 TCP/IP 提供程序，检测并处理每个上述条件。 此开关仅允许一个进程执行传输数据或更改基础的共享套接字的状态的操作一次。 进程动态交换控件的基础套接字，按照要求，将执行所请求的操作。 切换序列化操作不同进程共享的套接字上执行的请求和-先出 (FIFO) 顺序执行这些操作。 开关会等待所有正在进行中操作完成，然后交换到另一个进程基础套接字的控制。 在逻辑上，交换机会离开控制过程基础套接字的控制立即 noncontrolling 在过程请求符合要求的操作。 控件移走后，就像 noncontrolling 过程一样原始控制进程切换视为如果原始控制进程请求符合要求的操作。 请注意该交换机重复套接字句柄上执行任何操作直到 noncontrolling 过程实际上使用的数据传输或状态更改操作重复套接字句柄。

开关和相应的 SAN 服务提供程序都会加载到共享到特定的基础套接字的访问权限的所有进程。 开关会维护共享套接字的所有进程中其自己套接字上下文和连接状态信息。 SAN 服务提供程序时需要维护的时间可以控制基础套接字在任意给定时间的进程中仅其套接字上下文和连接状态信息。 SAN 服务提供程序必须交换其上下文和连接状态信息从当前控制进程到下一步控制进程的控制，每当开关需要交换下面的序列中所述。 为了尽量减少所需的交换的资源量，SAN 服务提供商可以维护其共享基础套接字的所有进程中的上下文和连接的状态信息。

由于交换机不会创建应用程序调用任一之前对应到应用程序套接字的 SAN 套接字**连接**或**侦听**函数，此开关不能请求的 SAN服务提供程序执行交换操作之前应用程序套接字连接或进行侦听。 即使应用程序套接字连接或侦听，以下条件之一之前必须满足该交换机请求之后 SAN 服务提供程序的套接字的交换控制：

-   不控制套接字的进程启动数据传输。 控制进程启动的所有数据传输操作都完成之前，SAN 服务提供商不交换的套接字的控件。

-   不控制套接字调用的进程**WSAAccept**， **WSPAccept**，或**AcceptEx**函数以启动侦听套接字上的连接接受操作。 SAN 服务提供商不交换的套接字的控件，直到所有接受控制进程启动的请求已完成。

开关将执行以下步骤来交换连接 SAN 的套接字从控制进程到下一步控制进程的控制 (有关概述的交换处理，请参阅的文档备注部分中的表[**WSPDuplicateSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff566282)函数。):

1.  开关控制过程中挂起来自应用程序的新请求的处理。 当所有发送和 RDMA SAN 套接字上进行的操作已完成时，此开关调用 SAN 服务提供商的[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316)函数将消息发送到已连接的对等方请求以在挂起会话和调用的 SAN 服务提供商[ **WSPDeregisterMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566279)函数，以释放所有本地缓冲区，用于发送操作。 在对等连接的交换机上 SAN 套接字，若要完成，正在进行中挂起的新的应用程序请求和等待所有发送和 RDMA 操作处理的结果，并释放所有 RDMA 的内存。 接下来，对等连接发送一个答复消息，指示在会话挂起。 收到以下确认消息，在本地终结点上的交换机调用 SAN 服务提供商**WSPDeregisterRdmaMemory**函数，以释放所有 RDMA 的内存。 此时，SAN 套接字连接这两个终结点只能具有接收申请处于挂起状态。 这些接收请求保持挂起状态以允许重新激活的会话的远程对等方的 SAN 套接字上。 在下一步中完成控制过程中在本地 SAN 套接字上的接收请求。 当挂起连接时，在远程对等连接队列新阻止或重叠的请求，切换到 SO 向上缓冲新非阻止发送\_SNDBUF 设置后达到缓冲区限制时，失败新非阻止发送和失败的所有新非阻止性将会收到包含 WSAEWOULDBLOCK。 控制进程中的本地交换机如同进程不具有的套接字控制处理应用程序套接字上的新请求。

2.  开关在会话挂起后，调用 SAN 服务提供商**WSPDuplicateSocket**控制进程直接 SAN 服务提供程序，从而将套接字上下文传输到的地址空间中的函数下一步控制过程。 开关指定中的下一步控制过程*dwProcessId*的参数**WSPDuplicateSocket**。 **WSPDuplicateSocket**函数必须调用**WPUCompleteOverlappedRequest**函数来完成所有未完成接收请求，成功状态，零字节的套接字上。 SAN 服务提供商必须也会自动释放与这些请求关联的所有缓冲区。 由于交换机不会请求后 SAN 套接字上的任何其他操作，SAN 服务提供程序释放所有缓冲区**WSPDuplicateSocket**返回。 唯一可能的例外是**WSPCloseSocket**函数调用下, 一步中所述。 之后**WSPDuplicateSocket**返回时，交换机将中的值**dwProviderReserved** WSAPROTOCOL 成员\_INFOW 结构*lpProtocolInfo*输出参数所指向。 此开关使用此值来标识基础套接字下, 一步控制进程的上下文中。 因此中的值**dwProviderReserved**必须用于在系统上的所有进程间唯一地标识基础套接字和该套接字连接。 此外，此值必须是仅在交换机中指定进程的上下文中有效*dwProcessId*的参数**WSPDuplicateSocket**。

3.  开关的套接字上下文传输到下一步控制进程的地址空间后，调用 SAN 服务提供商[ **WSPSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff566319)下一步控制的上下文中函数过程。 在此调用中，此开关将传递基础套接字中返回的值**WSPDuplicateSocket**调用**dwProviderReserved** WSAPROTOCOL 成员\_INFOW向其结构*lpProtocolInfo*输入参数所指向。 如果下一步控制进程没有请求 SAN 套接字的创建，SAN 服务提供商必须创建一个新的套接字并调用**WPUCreateSocketHandle**函数获取的句柄，所需的任何新的套接字。 如果在下一步控制进程的上下文中创建了 SAN 套接字，SAN 服务提供商可以重新激活以前套接字和返回以前使用的套接字的相同描述符。 在这种情况下，SAN 服务提供程序不应调用**WPUCreateSocketHandle**，但应继续使用该交换机提供的原始套接字句柄。 或者，SAN 服务提供商可以创建新的套接字，而不考虑一个套接字是否以前存在于该过程。 在这种情况下，该交换机必须调用 SAN 服务提供商[ **WSPCloseSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff566273)要释放的以前的套接字描述符的下一步控制进程的上下文中的函数。

4.  开关控制下一步的过程中重新启动应用程序中的新请求的处理。

不同之处在于该交换机不需要挂起会话，交换机类似的方式，在复制侦听套接字。 开关等待，直到它完成所有**WSPAccept**由应用程序的已启动的调用**接受**并**AcceptEx**调用 SAN 服务之前调用提供商**WSPDuplicateSocket**控制过程中的函数。

因为该交换机挂起之前调用 SAN 套接字上的新请求的处理 SAN 服务提供程序的**WSPDuplicateSocket**函数，SAN 服务提供程序可以发布与中的本地终结点相关联的所有资源控制进程。 SAN 服务提供商甚至可以终止基础连接。 如果 SAN 服务提供商关闭基础连接控制过程中的，SAN 服务提供商必须重新建立连接后切换调用 SAN 服务提供商**WSPSocket**函数中下一步控制过程。 之后**WSPSocket**调用返回时下, 一步控制进程内的 SAN 套接字必须位于相同的状态，从交换机的角度来看，因为控制进程中的 SAN 套接字调用 SAN 服务在切换之前提供商**WSPDuplicateSocket**函数。

如果 SAN NIC 支持在不同进程中运行的终结点之间共享资源，SAN 服务提供程序没有释放之前接收所控制执行过程中的本地终结点的资源**WSPDuplicateSocket**调用。 在这种情况下，与本地终结点相关联的 SAN 套接字保持前者控制过程中非活动状态直到交换机交换返回的下一步控制进程的套接字上下文或调用 SAN 服务提供商的**WSPCloseSocket**函数来显式关闭套接字。 因为大多数应用程序最初创建它-在过程中执行套接字到其最终访问通常以关闭连接-SAN 服务提供商可以提高性能如果 SAN 服务提供商保留的套接字上下文中控制进程后交换机交换到下一步控制进程的套接字的控制。

请注意，在所有情况下，SAN 套接字描述符必须保持有效，直到开关调用 SAN 服务提供商**WSPCloseSocket**函数来显式关闭套接字。 即使 SAN 服务提供程序释放所有资源中之前接收特定进程的套接字**WSPDuplicateSocket**调用中，SAN 服务提供商必须重复使用套接字描述符直到开关调用**WSPCloseSocket**上该描述符。

进程意外的退出或某些其他错误条件可能会中断 SAN 服务提供商的套接字复制操作。 例如，资源不足可能导致此类中断。 开关会将此类错误条件如同任何其他错误情况。 如有必要，切换将关闭与基础套接字中所有进程强制终止的套接字连接相关联的所有描述符。 如有可能，应完成的 SAN 服务提供程序的远程对等方[ **WSPRecv** ](https://msdn.microsoft.com/library/windows/hardware/ff566309)接收相应的错误代码，如 WSAECONNRESET 传入数据的调用。 此错误代码通知终止连接的远程对等方。 如果在远程对等方 switch 未收到此连接终止的指示，在远程对等方 switch 挂起连接如果超时请求挂起系统出现故障。

 

 





