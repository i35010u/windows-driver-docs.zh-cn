---
title: 事件命令
description: 事件命令
ms.assetid: e2b9f985-be57-49a9-b546-5cc74b0b061b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5236cebc751b1351d91e235df20941c6fbfec8fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370041"
---
# <a name="event-commands"></a>事件命令


## <span id="ddk_event_commands_si"></span><span id="DDK_EVENT_COMMANDS_SI"></span>


在本部分中的命令用于通过 microdriver 设备事件支持。

<span id="CMD_GET_INTERRUPT_EVENT"></span><span id="cmd_get_interrupt_event"></span>CMD\_获取\_中断\_事件  
调用 WIA 平板驱动程序在单独的线程来监视使用来自设备的中断的按钮事件的状态 (即，通过中断管道事件报告的 USB 设备的)。 如果你的设备仅支持轮询，此命令不需要实现，和 E\_NOTIMPL 应返回。

两个事件句柄传递给 microdriver。 **LVal**的成员[ **VAL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-val)结构保存应 microdriver 使用发送信号的事件句柄**SetEvent**按钮事件发生时的函数。 **处理**VAL 结构的成员将具有事件句柄，当正在卸载该驱动程序时将 WIA 平板驱动程序终止或关闭。

**PGuid** VAL 结构中的成员应设置为指向已推送的按钮的 GUID。 如果没有按钮曾按下，它应设置为 GUID\_NULL。

<span id="CMD_STI_GETSTATUS"></span><span id="cmd_sti_getstatus"></span>CMD\_STI\_GETSTATUS  
由 WIA 平板驱动程序添加到获取设备的联机状态以及设备是否具有普通按钮，以获取按钮状态调用。

设置**lVal**成员传递[ **VAL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-val)结构为 1，如果你的设备是否联机，并工作正常。 如果**lVal**设置为 1 以外的其他任何值，该设备被视为处于脱机状态，并且它将失败控制面板中的设备测试。

如果设备支持不使用来自设备的中断的按钮和按钮的按下**pGuid**传递 VAL 结构中的成员应设置为按钮事件的 GUID。 如果没有按钮按下，点**pGuid**的值为 GUID\_NULL。 这表示没有挂起的事件。

此命令是必需的如果设备支持轮询一次事件或者想要显示联机状态的设备。

 

 





