---
title: 在 WinDbg 中配置异常和事件
description: 你可以配置 WinDbg，以特定方式对指定的异常和事件做出反应。 对于每个异常，可以设置中断状态和处理状态。
ms.assetid: B91DD7B6-5206-4BA6-8B49-8ECCA2FA730B
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10c50d9012bda84a5a02afacfccb8b6c2cfda45b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524056"
---
# <a name="configuring-exceptions-and-events-in-windbg"></a>在 WinDbg 中配置异常和事件


你可以配置 WinDbg，以特定方式对指定的异常和事件做出反应。 对于每个异常，可以设置中断状态和处理状态。 对于每个事件，可以设置中断状态。

可以通过执行下列任一配置中断状态：

-   选择**事件筛选器**从**调试**菜单中，单击想要从列表中的事件**事件筛选器**对话框中，并选择**已启用**，**禁用**，**输出**，或**忽略**。

-   使用[ **SXE**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)， **SXD**， **SXN**，或**SXI**命令。

可以通过执行以下操作配置的处理状态：

-   选择**事件筛选器**从**调试**菜单中，单击想要从列表中的事件**事件筛选器**对话框中，并选择**已处理**或**未处理**。

-   使用[ **SXE**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)， **SXD**， **SXN**，或**SXI**命令。

有关异常和事件的详细讨论，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

 

 





