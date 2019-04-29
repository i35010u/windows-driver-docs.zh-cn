---
title: 客户端对象
description: 客户端对象
ms.assetid: 173a67f1-093e-4462-8e2c-41d0f10106d0
keywords:
- 调试器引擎，客户端对象
- 客户端对象
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6861c3e060420c1b66be6c8f11c7571d37c3a04
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375090"
---
# <a name="client-objects"></a>客户端对象


## <span id="client-objects"></span><span id="CLIENT_OBJECTS"></span>


与几乎所有交互[调试器引擎](introduction.md#debugger-engine)是通过*客户端对象*，通常只是称为*客户端*。 每个客户端提供的顶级引擎接口的实现。 每个接口提供了一组不同的方法，可用于与引擎，以及通过目标引擎进行交互。 引擎的实例可以有许多客户端，每个都有其自己的状态。

### <a name="span-idprimary-clientsspanspan-idprimaryclientsspanprimary-clients"></a><span id="primary-clients"></span><span id="PRIMARY_CLIENTS"></span>主要客户端

一个*主要客户端*客户端，已联接当前调试会话。 最初，创建一个新的客户端对象时，它不是主要的客户端。 客户端将成为主要的客户端时使用它来获取目标 (例如，通过调用[ **CreateProcess2**](https://msdn.microsoft.com/library/windows/hardware/ff539323)) 或连接到调试会话使用[ **ConnectSession**](https://msdn.microsoft.com/library/windows/hardware/ff539245)。 调试程序命令[ **.clients** ](-clients--list-debugging-clients-.md)列出了只有主客户端。

### <a name="span-idcallback-objectsspanspan-idcallbackobjectsspancallback-objects"></a><span id="callback-objects"></span><span id="CALLBACK_OBJECTS"></span>回调对象

可使用每个客户端注册的回调对象。 有三种类型的回调对象：

1.  **输入的回调对象**(或*输入回调*): 该引擎调用输入的回调以请求输入。 例如，控制台窗口与调试器无法注册为引擎提供来自用户输入的输入的回调或调试器可能会注册为引擎提供从文件输入的输入的回调。

2.  **输出回调对象**(或*输出回调*): 该引擎调用以显示输出的输出回调。 例如，控制台窗口与调试器无法注册向用户显示调试器的输出的输出回调或调试器可能注册将输出发送到日志文件的输出回调。

3.  **事件的回调对象**(或*事件的回调*): 该引擎调用事件的回调，每当事件发生在目标中 （或没有引擎的状态的更改）。 例如，调试程序扩展插件库无法注册一个事件回调来监视特定事件或特定事件发生时执行自动的操作。

### <a name="span-idremote-debuggingspanspan-idremotedebuggingspanremote-debugging"></a><span id="remote-debugging"></span><span id="REMOTE_DEBUGGING"></span>远程调试

客户端对象方便主机引擎的远程实例通信。 [ **DebugConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff540465)函数会创建连接到远程引擎实例的客户端对象; 通过注册的远程引擎和回调对象执行此客户端上调用的方法本地使用客户端将会调用远程引擎执行回调调用时。

### <a name="span-idadditional-informationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional-information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关创建和使用客户端对象的详细信息，请参阅[使用回调对象](using-callback-objects.md)。 有关注册的回调对象的详细信息，请参阅使用回调对象。

 

 





