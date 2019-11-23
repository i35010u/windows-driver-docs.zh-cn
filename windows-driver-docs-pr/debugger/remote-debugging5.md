---
title: 远程调试（调试器引擎）
description: 如果客户端与目标的通信是间接的，例如通过网络连接进行的，则会发生远程调试。
ms.assetid: e52cc5fb-9f10-415e-9fe8-6eba71daab6d
keywords:
- 调试器引擎，远程调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 314cfe2f612da63db01f4a686ed15467b06cb5d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834284"
---
# <a name="remote-debugging-debugger-engine"></a>远程调试（调试器引擎）


如果客户端与目标的通信是间接的，例如通过网络连接进行的，则会发生远程调试。 远程调试时，调试器引擎的多个实例可以参与调试目标。 但是，其中恰好有一个实例负责调试会话;此实例称为*主机引擎*。

有许多可能的配置：可以在主机引擎（智能客户端）或其他引擎实例（调试客户端）中创建客户端对象;主机引擎可以直接连接到目标（调试服务器）;或者，代理可以直接连接到目标（进程服务器和内核连接服务器）。

多个客户端可以同时连接到主机引擎。 主机引擎可以连接到同一调试会话中的多个目标。 或者，在客户端和主机引擎之间以及主机引擎与每个目标之间，可以有一个或多个代理。

智能客户端是直接与主机引擎通信的客户端对象。 调试客户端是通过调用[**DebugConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugconnect)创建的;客户端使用 RPC 调用（包括主机引擎对客户端的[回调对象](client-objects.md#callback-objects)的调用）与主机引擎进行通信。

调试服务器是直接与目标进行通信的引擎实例，也是主机引擎。 进程服务器和内核连接服务器直接与目标进行通信，而不是主机引擎。 主机引擎通过发送低级内存、处理器和操作系统请求来与进程服务器或内核连接服务器进行通信，并且服务器将返回结果。

**请注意**   用于内核调试的典型双计算机设置--其中一个计算机是目标，另一个主机计算机--不被视为远程调试，因为只有一个引擎实例（在主计算机上），并且它直接与目标通信。

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关执行远程调试的详细信息，请参阅[远程目标](remote-targets.md)。

 

 





