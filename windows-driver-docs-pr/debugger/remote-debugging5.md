---
title: 远程调试 （调试器引擎）
description: 远程调试发生时，目标是客户端的通信是间接的例如，通过网络连接。
ms.assetid: e52cc5fb-9f10-415e-9fe8-6eba71daab6d
keywords:
- 调试器引擎，远程调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80e17425462079d09e3f9b260d8bcd4a1f7a691e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544089"
---
# <a name="remote-debugging-debugger-engine"></a>远程调试 （调试器引擎）


远程调试发生时，目标是客户端的通信是间接的例如，通过网络连接。 当远程调试多个实例的调试器引擎可以涉及在调试目标。 但是，恰好一个这些实例是负责调试会话;此实例称为*主机引擎*。

有许多可能的配置： 可以在主机引擎 （智能客户端） 或引擎 （调试客户端）; 的不同实例中创建客户端对象主机引擎可以连接直接到目标 （调试服务器）;或代理服务器可以直接连接到目标 （进程服务器和内核连接服务器）。

多个客户端可以同时连接到主机引擎。 并在同一个调试会话中的主机引擎可以连接到多个目标。 （可选） 可以有一个或多个代理客户端主机引擎之间和主机引擎和每个目标之间。

智能客户端是直接与主机引擎进行通信的客户端对象。 通过调用创建调试客户端[ **DebugConnect**](https://msdn.microsoft.com/library/windows/hardware/ff540465); 与主机引擎使用表示该引擎的 API 中的方法调用的 RPC 调用的客户端通信 （包括调用的主机引擎对客户端[回调对象](client-objects.md#callback-objects))。

调试服务器是直接与目标进行通信，并且仍主机引擎的引擎实例。 进程服务器和内核连接服务器直接与目标进行通信，而不是主机引擎。 主机引擎与进程服务器或内核连接服务器，通信通过发送低级别的内存、 处理器和操作系统的请求，并且服务器发送回结果。

**请注意**  的内核调试-典型两台计算机安装其中一台计算机是目标和其他主机计算机中--不被视为是远程调试 （在主机计算机中） 引擎和它的一个实例原样直接与目标进行通信。

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关执行远程调试的详细信息，请参阅[远程目标](remote-targets.md)。

 

 





