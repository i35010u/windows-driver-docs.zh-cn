---
title: KD 连接服务器（内核模式）
description: KD 连接服务器（内核模式）
keywords:
- 通过 KD 连接服务器进行远程调试
- KD 连接服务器
- KD 连接服务器，概述
- '智能客户端 (内核模式) '
- KdSrv
- KdSrv，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: af31646968ca230e2324e49243199c19d3adf546
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783475"
---
# <a name="kd-connection-servers-kernel-mode"></a>KD 连接服务器（内核模式）


## <span id="ddk_kd_connection_servers_kernel_mode__dbg"></span><span id="DDK_KD_CONNECTION_SERVERS_KERNEL_MODE__DBG"></span>


通过 KD 连接服务器进行内核模式远程调试涉及到在服务器上运行称为 *KD 连接服务器* 的小型应用程序。 然后，在客户端上启动内核模式调试器。 由于此调试器将执行所有实际处理，因此它被称为 *智能客户端*。

适用于 Windows 的调试工具包包含一个名为 KdSrv 的 KD 连接服务器 ( # A0) 。

这两台计算机不需要运行相同版本的 Windows;它们可以运行任何版本的 Windows。 但是，在客户端上使用的调试器二进制文件和服务器上使用的 KdSrv 二进制文件必须来自用于 Windows 的调试工具包版本。 此方法不能用于转储文件调试。

若要设置此远程会话，请首先设置 KD 连接服务器，然后激活智能客户端。 任意数量的智能客户端都可以通过单个 KD 连接服务器运行，但它们必须连接到不同的内核调试会话。

本节包括：

[激活 KD 连接服务器](activating-a-kd-connection-server.md)

[搜索 KD 连接服务器](searching-for-kd-connection-servers.md)

[激活智能客户端（内核模式）](activating-a-smart-client--kernel-mode-.md)

[KD 连接服务器示例](kd-connection-server-examples.md)

[控制 KD 连接服务器会话](controlling-a-kd-connection-server-session.md)

 

 





