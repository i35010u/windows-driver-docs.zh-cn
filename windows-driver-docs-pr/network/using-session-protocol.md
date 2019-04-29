---
title: 使用会话协议
description: 使用会话协议
ms.assetid: 355286f9-ef85-4ba6-b21a-fc51e0b93fed
keywords:
- 会话协议 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72aa62121eb1546eaf41390f229e387aead420c9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373804"
---
# <a name="using-session-protocol"></a>使用会话协议





Windows 套接字开关使用其会话协议通过 SAN 连接传输数据。 如果交换机传输少量数据，它将控制消息中的数据传输。 每个控制消息由标头和应用程序数据的可选负载组成。 如果此开关要传输大量数据，它将使用 RDMA 操作这些数据传输。

本部分介绍如何设置和执行数据传输。

**请注意**  具体取决于加载该交换机的应用程序的行为，该开关来优化其会话协议来减少将应用程序数据传输所涉及的开销。

 

本部分还提供的交换机的会话协议数据传输的执行方式的示例。 但是，这些示例不包括这些操作的明确说明。

### <a name="setting-up-a-data-transfer"></a>设置数据传输

开关为每个连接的套接字分配的池的控制消息缓冲区。 开关然后会调用 SAN 服务提供商[ **WSPRegisterMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566311)函数来注册这些消息缓冲区的物理内存区域。 开关使用缓冲区池的一部分时调用 SAN 服务提供程序的流控制信息发送到远程对等方[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316)函数。 开关使用池中的其他部分来发布消息时调用 SAN 服务提供程序的远程对等方接收流控制信息的缓冲区[ **WSPRecv** ](https://msdn.microsoft.com/library/windows/hardware/ff566309)函数。 开关收到控制消息后，它立即使用它们。 使用控制消息后, 切换调用 SAN 服务提供商**WSPRecv**函数并传递接收缓冲区再次发布它们，以便他们可以从远程对等方接收更多控制消息。

### <a name="transferring-application-data"></a>将应用程序数据传输

数据传输的大小会影响开关将如何处理数据传输操作。

如果应用程序请求将发送少量数据，该交换机将这些数据传输中所述[发送 SAN 上的紧急数据](sending-urgent-data-on-a-san.md)。

如果应用程序请求将发送大量数据，此开关会将初始部分的数据复制到用于发送控制消息缓冲区。 此控制消息的标头包含用于指定应用程序的数据量的信息。 开关然后调用 SAN 服务提供商[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316)函数将此控制消息发送到 SAN 套接字的远程对等方。

如何切换完成的应用程序数据传输取决于服务提供程序是否支持[ **WSPRdmaRead** ](https://msdn.microsoft.com/library/windows/hardware/ff566304)函数。

### <a name="data-transfer-to-a-provider-that-supports-the-wsprdmaread-function"></a>将数据传输到的提供程序支持 WSPRdmaRead 函数

下图显示了如何切换完成的应用程序数据传输，如果 SAN 服务提供程序在远程对等方的概述支持 WSPRdmaRead 函数。 遵循序列描述将更多详细信息中的应用程序数据传输。

![远程对等方支持 wsprdmaread](images/wsprdmaread.png)

### <a name="to-transfer-data-when-the-remote-peer-supports-wsprdmaread"></a>若要将数据传输时远程对等方支持 WSPRdmaRead

-   本地交换机必须调用 SAN 服务提供商[ **WSPRegisterRdmaMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566313)函数以注册 RDMA 内存进行读访问。 在这种情况下，消息缓冲区的控制标头还标识包含该应用程序的剩余数据的 RDMA 内存的描述符。
-   开关在远程对等互连然后调用[ **WSPRdmaRead** ](https://msdn.microsoft.com/library/windows/hardware/ff566304)若要从 RDMA 内存的应用程序数据传输到接收在远程对等方 switch 以前注册的缓冲区[**WSPRegisterMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566311)调用。 SAN 服务提供程序在后台将缓冲的数据传输。 这样做使 SAN 服务提供程序发送缓冲的数据时，请勿将问题发布一次发布另一个的多个发送的应用程序发送请求。
-   开关在远程对等互连然后调用[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316)将控制消息发送到本地的开关，用于指示已完成传输。
-   本地切换调用[ **WSPDeregisterRdmaMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566281)函数，以释放 RDMA 的内存。
-   本地交换机完成应用程序发送请求。 如果此开关不能注册的应用程序的数据缓冲区的内存或如果不能完全分配临时内存，其完成后的应用程序发送请求， **WSAENOBUFS**错误代码。

### <a name="data-transfer-to-a-provider-that-does-not-support-the-wsprdmaread-function"></a>将数据传输到的提供程序不支持 WSPRdmaRead 函数

下图显示了如何切换完成的应用程序数据传输，如果在远程对等方的 SAN 服务提供程序不支持的概述[ **WSPRdmaRead** ](https://msdn.microsoft.com/library/windows/hardware/ff566304)函数。 遵循序列描述将更多详细信息中的应用程序数据传输。

![远程对等方不支持 wsprdmaread](images/wsprdmaread2.png)

### <a name="to-transfer-data-when-the-remote-peer-does-not-support-wsprdmaread"></a>当远程对等方不支持 WSPRdmaRead 传输数据

-   在远程对等方调用开关[ **WSPRegisterRdmaMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566313)注册 RDMA 内存以进行写访问。
-   开关在远程对等互连然后调用[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316)将控制消息发送到本地开关，RDMA 内存本地开关可以写入的位置。
-   本地切换调用[ **WSPRdmaWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff566306)函数将应用程序数据传输到 RDMA 内存。 SAN 服务提供程序在后台将缓冲的数据传输。 这样做使 SAN 服务提供程序发送缓冲的数据时，请勿将问题发布一次发布另一个的多个发送的应用程序发送请求。
-   本地切换调用[ **WSPGetOverlappedResult** ](https://msdn.microsoft.com/library/windows/hardware/ff566288)函数获取传输的结果。 有关详细信息，请参阅[完成数据传输请求](completing-data-transfer-requests.md)。
-   本地切换调用[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316)将控制消息发送到远程对等方，来指示传输已完成。
-   在远程对等方调用开关[ **WSPDeregisterRdmaMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566281)以释放 RDMA 的内存。
-   本地交换机完成应用程序发送请求。 如果此开关不能注册的应用程序的数据缓冲区的内存或如果不能分配临时内存，则其完成后的应用程序发送请求， **WSAENOBUFS**错误代码。

## <a name="related-topics"></a>相关主题


[在 SAN 上传输数据](transferring-data-on-a-san.md)

 

 






