---
title: 客户端对象
description: 客户端对象
ms.assetid: 173a67f1-093e-4462-8e2c-41d0f10106d0
keywords:
- 调试器引擎，客户端对象
- 客户端对象
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15b22ddb8039fe1c602be46b9e82e1dac10a644e
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242822"
---
# <a name="client-objects"></a>客户端对象


## <span id="client-objects"></span><span id="CLIENT_OBJECTS"></span>


几乎所有与[调试器引擎](introduction.md#debugger-engine)的交互都是通过*客户端对象*进行的，通常只是指*客户*端。 每个客户端都提供顶层引擎接口的实现。 每个接口都提供一组不同的方法，这些方法可用于与引擎进行交互，以及通过引擎与目标进行交互。 一个引擎实例可以有许多客户端，每个客户端都有自己的状态。

### <a name="span-idprimary-clientsspanspan-idprimary_clientsspanprimary-clients"></a><span id="primary-clients"></span><span id="PRIMARY_CLIENTS"></span>主客户端

*主客户端*是已联接当前调试会话的客户端。 最初，当创建新的客户端对象时，该对象不是主客户端。 当客户端用于获取目标（例如，通过调用[**CreateProcess2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess2)）或连接到使用[**ConnectSession**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-connectsession)的调试会话时，客户端将成为主客户端。 调试器命令[ **。客户端**](-clients--list-debugging-clients-.md)仅列出主客户端。

### <a name="span-idcallback-objectsspanspan-idcallback_objectsspancallback-objects"></a><span id="callback-objects"></span><span id="CALLBACK_OBJECTS"></span>回调对象

可以向每个客户端注册回调对象。 有三种类型的回调对象：

1.  **输入回调对象**（或*输入回调*）：引擎调用输入回调来请求输入。 例如，具有控制台窗口的调试器可以注册输入回调以向引擎提供用户的输入，或者调试器可以注册输入回调以向引擎提供来自文件的输入。

2.  **输出回调对象**（或*输出回调*）：引擎调用输出回调以显示输出。 例如，具有控制台窗口的调试器可以注册输出回调以向用户显示调试器的输出，或者，调试器可以注册输出回调以将输出发送到日志文件。

3.  **事件回调对象**（或*事件回调*）：只要目标中发生事件（或引擎状态发生更改），引擎就会调用事件回调。 例如，在发生特定事件时，调试器扩展库可以注册事件回调来监视某些事件或执行自动操作。

### <a name="span-idremote-debuggingspanspan-idremote_debuggingspanremote-debugging"></a><span id="remote-debugging"></span><span id="REMOTE_DEBUGGING"></span>远程调试

客户端对象便于与主机引擎的远程实例进行通信。 [**DebugConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugconnect)函数创建连接到远程引擎实例的客户端对象;在此客户端上调用的方法由远程引擎执行，当远程引擎进行回调调用时，将调用使用客户端本地注册的回调对象。

### <a name="span-idadditional-informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional-information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关创建和使用客户端对象的详细信息，请参阅[使用回叫对象](using-callback-objects.md)。 有关注册回调对象的详细信息，请参阅使用回叫对象。

 

 





