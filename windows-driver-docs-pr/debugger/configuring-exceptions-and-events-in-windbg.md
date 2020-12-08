---
title: 在 WinDbg 中配置异常和事件
description: 您可以将 WinDbg 配置为以特定方式响应指定的异常和事件。 对于每个异常，可以设置中断状态和处理状态。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 056c0a971b68880b294b8a1e593f6d6ffbd45948
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821573"
---
# <a name="configuring-exceptions-and-events-in-windbg"></a>在 WinDbg 中配置异常和事件


您可以将 WinDbg 配置为以特定方式响应指定的异常和事件。 对于每个异常，可以设置中断状态和处理状态。 对于每个事件，可以设置中断状态。

可以通过执行下列操作之一来配置中断状态：

-   从 "**调试**" 菜单中选择 "**事件筛选器**"，从 "**事件筛选器**" 对话框中的列表中单击所需的事件，然后选择 "**已启用**"、"**禁用**"、"**输出**" 或 "**忽略**"。

-   使用 [**SXE**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)、 **SXD**、 **SXN** 或 **SXI** 命令。

可以通过执行下列操作之一来配置处理状态：

-   从 "**调试**" 菜单中选择 "**事件筛选器**"，从 "**事件筛选器**" 对话框中的列表中单击所需的事件，然后选择 "已 **处理**" 或 "**未处理**"。

-   使用 [**SXE**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)、 **SXD**、 **SXN** 或 **SXI** 命令。

有关异常和事件的详细讨论，请参阅 [控制异常和事件](controlling-exceptions-and-events.md)。

 

 





