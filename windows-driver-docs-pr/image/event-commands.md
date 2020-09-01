---
title: 事件命令
description: 事件命令
ms.assetid: e2b9f985-be57-49a9-b546-5cc74b0b061b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 062b3608c91284d8b755104a4c376d0bdc43f6e3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192955"
---
# <a name="event-commands"></a>事件命令


## <span id="ddk_event_commands_si"></span><span id="DDK_EVENT_COMMANDS_SI"></span>


此部分中的命令由 microdriver for device 事件支持使用。

<span id="CMD_GET_INTERRUPT_EVENT"></span><span id="cmd_get_interrupt_event"></span>CMD \_ 获取 \_ 中断 \_ 事件  
由 WIA 平板驱动程序在单独的线程中调用，以监视使用来自设备的中断的按钮事件的状态， (即，对于通过中断管道报告事件的 USB 设备) 。 如果设备仅支持轮询，则不需要实现此命令，而 \_ 应返回 E NOTIMPL。

将两个事件句柄传递到 microdriver。 [**VAL**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)结构的**lVal**成员保存事件句柄，该句柄应在按钮事件发生时使用**SetEvent**函数通过 microdriver 进行通知。 VAL 结构的 **handle** 成员保存一个事件句柄，该句柄将在卸载或关闭驱动程序时由 WIA 平板驱动程序发出信号。

VAL 结构的 **pGuid** 成员应设置为指向已推送的按钮的 GUID。 如果未按下任何按钮，则应将其设置为 GUID \_ NULL。

<span id="CMD_STI_GETSTATUS"></span><span id="cmd_sti_getstatus"></span>CMD \_ STI \_ GETSTATUS  
由 WIA 平板驱动程序调用以获取设备的联机状态，并且如果设备具有推送按钮，则获取按钮状态。

如果设备处于联机状态并且正常运行，则将传递的[**VAL**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)结构的**lVal**成员设置为1。 如果将 **lVal** 设置为除1之外的任何值，则设备将被视为处于脱机状态，并且在 "控制面板" 中将无法进行设备测试。

如果设备支持不使用设备中断的按钮并按下了按钮，则传递的 VAL 结构的 **pGuid** 成员应设置为按钮事件的 GUID。 如果未按下任何按钮，请将 **pGuid** 指向值 GUID \_ NULL。 这表明没有挂起的事件。

如果设备支持轮询事件或你希望设备显示联机状态，则需要此命令。

 

