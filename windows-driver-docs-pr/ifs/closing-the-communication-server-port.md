---
title: 关闭通信服务器端口
description: 关闭通信服务器端口
ms.assetid: 43dfa162-0098-4a9b-9272-9da429cb0108
keywords:
- 通信服务器端口 WDK 文件系统微筛选器
- 端口 WDK，文件系统微筛选器
- 关闭通信服务器端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ea9e306dc9c8a1a5c718e50f89da148964917bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566883"
---
# <a name="closing-the-communication-server-port"></a>关闭通信服务器端口


## <span id="ddk_closing_the_communication_server_port_if"></span><span id="DDK_CLOSING_THE_COMMUNICATION_SERVER_PORT_IF"></span>


如果微筛选器驱动程序通过调用以前打开的内核模式下通信服务器端口[ **FltCreateCommunicationPort**](https://msdn.microsoft.com/library/windows/hardware/ff541931)，它必须通过调用关闭端口[ **FltCloseCommunicationPort**](https://msdn.microsoft.com/library/windows/hardware/ff541871)。 若要防止系统微筛选器驱动程序在卸载过程中，挂起[ **FilterUnloadCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff551085)例程必须关闭然后再调用此端口[ **FltUnregisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544606)。

如果在用户模式应用程序到通信服务器端口已打开的连接，该连接任何客户端端口保持打开状态的后[ **FltCloseCommunicationPort** ](https://msdn.microsoft.com/library/windows/hardware/ff541871)返回。 但是，筛选器管理器将卸载微筛选器驱动程序时关闭客户端的任何端口。

 

 




