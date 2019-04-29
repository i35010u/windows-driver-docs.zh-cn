---
title: KD 连接服务器（内核模式）
description: KD 连接服务器（内核模式）
ms.assetid: fe0c9110-8fbf-46ae-ae1d-75ab5231aef3
keywords:
- 通过 KD 连接服务器的远程调试
- KD 连接服务器
- KD 连接服务器概述
- 智能客户端 （内核模式）
- KdSrv
- KdSrv 概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb2bbe052ff4908935984bcd3b84a14dd5d41d4e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367203"
---
# <a name="kd-connection-servers-kernel-mode"></a>KD 连接服务器（内核模式）


## <span id="ddk_kd_connection_servers_kernel_mode__dbg"></span><span id="DDK_KD_CONNECTION_SERVERS_KERNEL_MODE__DBG"></span>


运行名为的小型应用程序内核模式远程调试通过 KD 连接服务器涉及*KD 连接服务器*在服务器上。 然后在客户端上启动内核模式调试程序。 由于此调试器将执行所有实际的处理，调用*智能客户端*。

有关 Windows 调试工具软件包包含名为 KdSrv (kdsrv.exe) KD 连接服务器。

两台计算机不需要运行相同版本的 Windows;它们可以运行任何版本的 Windows。 但是，客户端上使用的调试程序二进制文件和在服务器上使用 KdSrv 二进制文件必须来自同一版本的 Windows 调试工具软件包。 此方法不能用于调试转储文件。

若要设置此远程会话，KD 连接服务器设置第一个，并智能客户端激活。 任意数量的智能客户端可以通过单个 KD 连接服务器，运行，但他们必须每个连接到不同的内核调试会话。

本部分包括：

[激活 KD 连接服务器](activating-a-kd-connection-server.md)

[正在搜索 KD 连接服务器](searching-for-kd-connection-servers.md)

[激活智能客户端 （内核模式）](activating-a-smart-client--kernel-mode-.md)

[KD 连接服务器示例](kd-connection-server-examples.md)

[控制 KD 连接服务器会话](controlling-a-kd-connection-server-session.md)

 

 





