---
title: 使用 Repeater
description: 使用 Repeater
ms.assetid: c6904b6d-f28b-4494-95d0-9e6fc3dc10f3
keywords:
- repeater，使用 repeater
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bd5f3757abab3dcbfeb266cb73749107ecf4c18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554865"
---
# <a name="using-a-repeater"></a>使用 Repeater


## <span id="ddk_using_a_repeater_dbg"></span><span id="DDK_USING_A_REPEATER_DBG"></span>


Repeater 连接遵循非常简单的规则：

-   对于每个其他计划的服务器和客户端的任何通信通过无需更改 repeater。

-   对于传输连接该服务器执行任何操作会影响 repeater （和仅间接影响客户端）。

-   对于传输连接的客户端执行任何操作会影响 repeater （和仅间接影响服务器）。

这意味着任何调试命令，调试器输出，控制键和文件访问将进行完全像直接连接的客户端和服务器。 Repeater 将对所有这些命令不可见。

终止连接本身的操作将会影响 repeater。 例如，如果您发出[ **qq (Quit)** ](q--qq--quit-.md)命令从客户端，服务器将关闭，并且会向传输发送到关闭信号。 这将导致 repeater 退出 (除非与用于启动 **-p**选项)。 作为另一个示例中， [ **.clients （列表调试客户端）** ](-clients--list-debugging-clients-.md)命令将列出客户端的计算机名称，但它会显示用于与中继器连接服务器的连接协议。

如果在服务器关闭的情况下，将自动退出 repeater (除非与用于启动 **-p**选项)。 Repeater 当关闭时，这将导致调试客户端中，若要退出，尽管智能客户端将不会。 如果出于某种原因需要直接终止 repeater，您可以使用任务管理器或 kill.exe 工具。

 

 





