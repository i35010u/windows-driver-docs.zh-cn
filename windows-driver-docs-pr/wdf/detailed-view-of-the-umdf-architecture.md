---
title: UMDF 的体系结构
description: 本主题介绍如何驱动程序管理器生成用户模式设备堆栈和主机进程、 reflector 和驱动程序管理器如何处理应用程序发送到用户模式驱动程序框架 (UMDF) 驱动程序的 I/O 请求。
ms.assetid: 118e5fe8-ba1e-4012-9632-fd92f4cee6f1
keywords:
- 用户模式驱动程序框架 WDK，体系结构
- UMDF WDK，体系结构
- 用户模式驱动程序 WDK UMDF，体系结构
- 体系结构 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb66dd12ef53c0176016e36aa09f3a3850a4f16f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542924"
---
# <a name="architecture-of-umdf"></a>UMDF 的体系结构


本主题介绍如何驱动程序管理器生成用户模式设备堆栈和主机进程、 reflector 和驱动程序管理器如何处理应用程序发送到用户模式驱动程序框架 (UMDF) 驱动程序的 I/O 请求。

类似于内核模式堆栈，构造和拆解的用户模式堆栈是插 (PnP) 事件驱动。 生成内核模式堆栈后，该发送程序通知的驱动程序管理器启动的用户模式堆栈的构造。 驱动程序管理器会启动驱动程序主机进程，并提供到启动进程，以生成用户模式堆栈的足够信息。 这样一来，用户模式堆栈可被视为内核模式堆栈的扩展。

驱动程序主机进程提供用于用户模式下的执行环境之间的用户模式堆栈中的驱动程序的驱动程序和路由消息。 该发送程序使用基于消息的进程间通信机制来与驱动程序管理器和主机进程通信。

![umdf 组件包括向上和向下发送程序中的设备对象](images/umdfarch4.gif)

若要将 I/O 请求发送到 UMDF 驱动程序，应用程序调用 Win32 文件 I/O 函数，如[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)， **ReadFileEx**， **CancelIoEx**，或[ **DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)。 时该发送程序收到请求时从客户端应用程序，它将请求发送到相应的驱动程序主机进程。 驱动程序宿主进程然后路由到正确的用户模式设备堆栈顶部的请求。

该请求由一个用户模式堆栈中的驱动程序已完成，或者转发回该发送程序的驱动因素之一。 当反射器收到请求时从用户模式驱动程序堆栈时，它将向完成的内核模式堆栈下请求发送。

 

 





