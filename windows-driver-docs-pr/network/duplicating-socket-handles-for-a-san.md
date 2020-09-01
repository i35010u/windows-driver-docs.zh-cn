---
title: 复制 SAN 的套接字句柄
description: 复制 SAN 的套接字句柄
ms.assetid: d8e8cb6d-fcdb-4121-9a44-a2bc884ab620
keywords:
- Windows 套接字直接 WDK，套接字句柄
- SAN 套接字 WDK，复制套接字句柄
- 挂起 WDK Windows 套接字直通
- 复制套接字处理 WDK San
- 共享基础套接字 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 871c2a0bc34196bf6261778341272e42a921abee
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212205"
---
# <a name="duplicating-socket-handles-for-a-san"></a>复制 SAN 的套接字句柄





多个在不同进程中运行的应用程序可以使用 Windows 套接字交换机在共享的基础套接字上执行操作。 然而，一次只能有一个应用程序可以对该共享的基础套接字执行操作。

若要使用共享的基础套接字，应用程序必须通过以下方法之一检索该基础套接字的重复句柄：

-   直接调用 Windows Socket **WSADuplicateSocket** 函数

    在控制过程的上下文中进行调用， (在其中创建套接字) 的进程。

-   通过调用 Win32 DuplicateHandle 函数间接

    在 noncontrolling 进程的上下文中进行的调用 (，而不是创建套接字) 的进程。

-   使用句柄继承机制

    Noncontrolling 进程 (的子进程) 继承其父进程中创建的所有或某些句柄 (控制过程) 。

-   正常连接关闭期间

    如果控制进程中的应用程序关闭套接字并在仍有某些数据仍在发送时退出，则会在 Windows 套接 DLL 中缓冲剩余的数据。 系统服务进程上下文中的另一个应用程序 (noncontrolling 进程) 随后将发送此数据。

Windows 套接字交换机与 TCP/IP 提供程序一起检测并处理上述每个条件。 开关一次只允许一个进程执行传输基础共享套接字的数据或更改状态的操作。 根据需要，处理基础套接字的动态交换控制以执行请求的操作。 开关序列化不同进程请求在共享套接字上执行的操作，并在先进先出 (FIFO) 顺序中执行这些操作。 切换将等待所有正在进行的操作完成，然后将基础套接字的控制交换到另一个进程。 从逻辑上说，一旦 noncontrolling 的进程请求了限定操作，此开关就会立即控制基础套接字。 离开控制后，如果原始控制过程请求限定操作，则开关将处理原始控制过程，如 noncontrolling 进程。 请注意，在 noncontrolling 进程实际使用重复的套接字句柄进行数据传输或状态更改操作之前，此开关不会对重复的套接字句柄执行任何操作。

交换机和相应的 SAN 服务提供程序都将加载到所有共享访问特定基础套接字的进程中。 开关在共享套接字的所有进程中维护自己的套接字上下文和连接状态信息。 只有在任何给定时间点都控制基础套接字的进程中，SAN 服务提供程序才需要维护其套接字上下文和连接状态信息。 每当交换机需要交换时，SAN 服务提供程序必须将其上下文和连接状态信息的控制从当前控制过程中调换到下一控制过程，如以下序列中所述。 为了最大限度地减少交换所需的资源量，SAN 服务提供程序可以在共享基础套接字的所有进程中维护其上下文和连接状态信息。

由于在应用程序调用 **connect** 或 **侦听** 函数之前，此开关不会创建对应于应用程序套接字的 SAN 套接字，因此该开关无法请求 san 服务提供程序在应用程序套接字连接或侦听之前执行交换操作。 即使在应用程序套接字已连接或正在侦听后，必须满足以下条件之一，然后交换机才能请求 SAN 服务提供程序对套接字进行交换控制：

-   不控制套接字的进程会启动数据传输。 SAN 服务提供程序不会在控制进程已完成的所有数据传输操作完成之前，对套接字进行交换控制。

-   不控制套接字的进程会调用 **WSAAccept**、 **WSPAccept**或 **AcceptEx** 函数来启动侦听套接字上的连接接受操作。 SAN 服务提供程序不会在控制进程已完成的所有接受请求完成之前，对套接字进行交换控制。

此开关执行以下步骤，以将已连接的 SAN 套接字的控制从控制进程交换到下一个控制过程 (有关交换过程的概述，请参阅 [**WSPDuplicateSocket**](/previous-versions/windows/hardware/network/ff566282(v=vs.85)) 函数文档的 "备注" 部分中的表。 ) ：

1.  此开关在控制过程中暂停处理来自应用程序的新请求。 当 SAN 套接字上正在进行的所有发送和 RDMA 操作都已完成时，交换机将调用 SAN 服务提供程序的 [**WSPSend**](/previous-versions/windows/hardware/network/ff566316(v=vs.85)) 函数，以将消息发送到已连接的对等方，请求挂起会话并调用 SAN 服务提供程序的 [**WSPDeregisterMemory**](/previous-versions/windows/hardware/network/ff566279(v=vs.85)) 函数来释放用于发送操作的所有本地缓冲区。 因此，对等连接的交换机会挂起对新应用程序请求的处理，等待 SAN 套接字上正在进行的所有发送和 RDMA 操作完成，并释放所有 RDMA 内存。 接下来，对等连接将发送一条回复消息，指示该会话已挂起。 收到此确认消息后，本地终结点上的开关会调用 SAN 服务提供程序的 **WSPDeregisterRdmaMemory** 函数，以释放所有 RDMA 内存。 此时，连接的两个终结点上的 SAN 套接字只能有等待的接收请求。 这些接收请求在远程对等机的 SAN 套接字上保持挂起状态，以允许会话的重新激活。 在下一步中完成了控制过程中本地 SAN 套接字上的接收请求。 当连接处于挂起状态时，远程对等连接上的交换机将排队新的阻塞或重叠请求，缓冲区新的非阻止性发送到 \_ SNDBUF 设置，在达到缓冲区限制后将无法发送新的非阻止性发送，并使所有新的非阻止接收和 WSAEWOULDBLOCK 失败。 控制过程中的本地开关将处理应用程序套接字上的新请求，就好像该进程没有对套接字的控制一样。

2.  挂起会话后，交换机会在控制过程中调用 SAN 服务提供程序的 **WSPDuplicateSocket** 函数，以指示 san 服务提供程序将套接字上下文传输到下一个控制进程的地址空间中。 开关在**WSPDuplicateSocket**的*dwProcessId*参数中指定下一个控制进程。 **WSPDuplicateSocket**函数必须调用**WPUCompleteOverlappedRequest**函数，以在成功状态为0字节的情况上完成所有未完成的接收请求。 SAN 服务提供程序还必须自动释放与这些请求关联的所有缓冲区。 SAN 服务提供程序释放所有缓冲区，因为在 **WSPDuplicateSocket** 返回后，此开关不会在 SAN 套接字上请求更多操作。 唯一可能的例外是 **WSPCloseSocket** 函数调用，如下面的步骤所述。 **WSPDuplicateSocket**返回后，开关会将值保存在**dwProviderReserved** \_ *lpProtocolInfo*输出参数指向的 WSAPROTOCOL INFOW 结构的 dwProviderReserved 成员中。 开关使用此值在下一个控制过程的上下文中标识基础套接字。 因此， **dwProviderReserved** 中的值必须唯一标识该套接字在系统上所有进程中的基础套接字和连接。 此外，此值必须仅在在**WSPDuplicateSocket**的*dwProcessId*参数中指定的进程的上下文中有效。

3.  将套接字上下文传输到下一控制进程的地址空间后，交换机会在下一个控制过程的上下文中调用 SAN 服务提供程序的 [**WSPSocket**](/previous-versions/windows/hardware/network/ff566319(v=vs.85)) 函数。 在此调用中，开关将在**WSPDuplicateSocket**调用中返回的基础套接字的值传递给**dwProviderReserved** \_ *lpProtocolInfo*输入参数指向的 WSAPROTOCOL INFOW 结构的 dwProviderReserved 成员。 如果下一个控制过程未请求创建 SAN 套接字，则 SAN 服务提供程序必须创建新的套接字，并调用 **WPUCreateSocketHandle** 函数以获取句柄，这是任何新套接字所需的。 如果在下一控制过程的上下文中创建了 SAN 套接字，则 SAN 服务提供程序可以重新激活以前的套接字，并为以前使用的套接字返回相同的描述符。 在这种情况下，SAN 服务提供商不应调用 **WPUCreateSocketHandle**，但应继续使用交换机提供的原始套接字句柄。 或者，SAN 服务提供程序可以创建新的套接字，而不管先前是否在进程中存在该套接字。 在这种情况下，开关必须在下一个控制进程的上下文中调用 SAN 服务提供程序的 [**WSPCloseSocket**](/previous-versions/windows/hardware/network/ff566273(v=vs.85)) 函数，以释放以前的套接字说明符。

4.  此开关在下一控制过程中重新开始处理来自应用程序的新请求。

开关以类似的方式复制侦听套接字，只不过不需要该开关来挂起会话。 此开关将等待，直到它完成由应用程序的**accept**和**AcceptEx**调用启动的所有**WSPAccept**调用，然后才能在控制过程中调用 SAN 服务提供程序的**WSPDuplicateSocket**函数。

由于在调用 SAN 服务提供程序的 **WSPDuplicateSocket** 函数之前，此开关在 san 套接字上挂起了对新请求的处理，因此 SAN 服务提供程序可以在控制过程中释放与本地终结点相关联的所有资源。 SAN 服务提供商甚至可以终止基础连接。 如果 SAN 服务提供程序在控制过程中关闭基础连接，则在下一控制过程中，SAN 服务提供程序必须重新建立连接，然后再调用 SAN 服务提供程序的 **WSPSocket** 函数。 **WSPSocket**调用返回后，下一控制过程中的 san 套接字必须处于相同的状态，即从交换机的角度来看，因为控制进程中的 san 套接字早于调用 SAN 服务提供程序的**WSPDuplicateSocket**函数。

如果 SAN NIC 支持在不同进程中运行的终结点之间共享资源，则在接收 **WSPDuplicateSocket** 调用之前，san 服务提供程序不必为控制过程中的本地终结点释放资源。 在这种情况下，与本地终结点关联的 SAN 套接字在以前控制的进程中保持不活动状态，直到交换机从下一个控制进程交换套接字上下文，或调用 SAN 服务提供程序的 **WSPCloseSocket** 函数来显式关闭套接字。 由于大多数应用程序会在最初创建它的进程中对套接字执行最终访问（通常是关闭连接），因此，如果 SAN 服务提供程序在将套接字交换控制到下一控制过程后，SAN 服务提供程序在控制过程中保留套接字上下文，则 SAN 服务提供商可以提高性能。

请注意，在所有情况下，SAN 套接字描述符必须保持有效，直到交换机调用 SAN 服务提供程序的 **WSPCloseSocket** 函数以显式关闭套接字。 即使 SAN 服务提供程序在接收 **WSPDuplicateSocket** 调用之前释放特定进程中的套接字的所有资源，san 服务提供程序也不能重复使用套接字的描述符，直到交换机在该描述符上调用 **WSPCloseSocket** 。

意外进程退出或其他错误情况可能会中断 SAN 服务提供程序的套接字复制操作。 例如，资源不足会导致此类中断。 交换机会处理此类错误情况，因为它会执行任何其他错误情况。 如有必要，开关会关闭所有进程中与基础套接字关联的所有描述符，以强制终止套接字的连接。 如果可能，远程对等机上的 SAN 服务提供商应完成使用相应错误代码（如 WSAECONNRESET）接收传入数据的 [**WSPRecv**](/previous-versions/windows/hardware/network/ff566309(v=vs.85)) 调用。 此错误代码通知远程对等连接终止。 如果远程对等节点上的开关未接收到此连接-终止指示，则当请求挂起的系统失败时，远程对等节点上的切换会超时挂起的连接。

 

