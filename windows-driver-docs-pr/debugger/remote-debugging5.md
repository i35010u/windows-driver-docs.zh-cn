---
title: " (调试器引擎的远程调试) "
description: 如果客户端与目标的通信是间接的，例如通过网络连接进行的，则会发生远程调试。
ms.assetid: e52cc5fb-9f10-415e-9fe8-6eba71daab6d
keywords:
- 调试器引擎，远程调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02314abaaf78f55a4843183d72b3939a0bc7b464
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206799"
---
# <a name="remote-debugging-debugger-engine"></a> (调试器引擎的远程调试) 


如果客户端与目标的通信是间接的，例如通过网络连接进行的，则会发生远程调试。 远程调试时，调试器引擎的多个实例可以参与调试目标。 但是，其中恰好有一个实例负责调试会话;此实例称为 *主机引擎*。

有许多可能的配置：可以在主机引擎中创建客户端对象， (智能客户端) 或 (调试客户端的引擎的其他实例) ;主机引擎可以直接连接到目标 (调试服务器) ;或者，代理可以直接连接到目标 (进程服务器和内核连接服务器) 。

多个客户端可以同时连接到主机引擎。 主机引擎可以连接到同一调试会话中的多个目标。 或者，在客户端和主机引擎之间以及主机引擎与每个目标之间，可以有一个或多个代理。

智能客户端是直接与主机引擎通信的客户端对象。 调试客户端是通过调用 [**DebugConnect**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugconnect)创建的;客户端使用 RPC 调用（表示引擎的 API 中的方法调用）与主机引擎通信， (包括主机引擎对客户端的 [回调对象](client-objects.md#callback-objects)) 所做的调用。

调试服务器是直接与目标进行通信的引擎实例，也是主机引擎。 进程服务器和内核连接服务器直接与目标进行通信，而不是主机引擎。 主机引擎通过发送低级内存、处理器和操作系统请求来与进程服务器或内核连接服务器进行通信，并且服务器将返回结果。

**注意**   用于内核调试的典型双计算机设置--其中一台计算机是目标，另一台计算机不被视为远程调试，因为在主) 计算机上只有一个引擎 (实例，并且它直接与目标通信。

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关执行远程调试的详细信息，请参阅 [远程目标](remote-targets.md)。

 

