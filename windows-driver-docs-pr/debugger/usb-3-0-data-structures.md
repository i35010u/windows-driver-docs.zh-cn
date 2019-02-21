---
title: USB 3.0 数据结构
description: 本主题介绍使用 USB 3.0 主机控制器驱动程序的数据结构。
ms.assetid: 39BD7413-48A5-4199-BA8E-D2A77E4D23F1
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e51c35d47e1bd4590fb18515f183bf40ff530755
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533161"
---
# <a name="usb-30-data-structures"></a>USB 3.0 数据结构


本主题介绍使用 USB 3.0 主机控制器驱动程序的数据结构。 了解这些数据结构将有助于您使用[USB 3.0](usb-3-extensions.md)并[RCDRKD](rcdrkd-extensions.md)有效地调试器扩展命令。 此处提供的数据结构具有与一致的名称[USB 3.0 规范](https://go.microsoft.com/fwlink/p?LinkID=224892)。 熟悉了 USB 3.0 规范将进一步增强扩展命令用于调试 USB 3.0 驱动程序的能力。

USB 3.0 主机控制器驱动程序是 USB 3.0 核心驱动程序堆栈的一部分。 有关详细信息，请参阅[USB 驱动程序堆栈体系结构](https://go.microsoft.com/fwlink/p?LinkID=251983)。

每个 USB 3.0 主机控制器可以多达 255 设备，并且每个设备可以有最多 31 终结点。 下图显示了一些代表一个主控制器和已连接的设备的数据结构。

![表示一个主控制器和有槽和终结点上下文，又具有设备上下文的连接的设备的 usb 3.0 数据结构](images/usb3structures01.png)

## <a name="span-iddevicecontextbasearrayspanspan-iddevicecontextbasearrayspanspan-iddevicecontextbasearrayspandevice-context-base-array"></a><span id="Device_Context_Base_Array"></span><span id="device_context_base_array"></span><span id="DEVICE_CONTEXT_BASE_ARRAY"></span>设备上下文基础数组


设备上下文基础数组是指向设备上下文结构的指针的数组。 没有为每个设备连接到主控制器的一个设备上下文结构。 元素 1 到 255 指向设备上下文结构。 元素 0 分到主控制器的上下文结构。

## <a name="span-iddevicecontextandslotcontextspanspan-iddevicecontextandslotcontextspanspan-iddevicecontextandslotcontextspandevice-context-and-slot-context"></a><span id="Device_Context_and_Slot_Context"></span><span id="device_context_and_slot_context"></span><span id="DEVICE_CONTEXT_AND_SLOT_CONTEXT"></span>设备上下文和槽上下文


设备上下文结构保存到终结点上下文结构的指针的数组。 没有在设备上的每个终结点的一个终结点上下文结构。 元素 1 到 31 指向终结点上下文结构。 元素 0 分到某个槽上下文结构，其中包含设备的上下文信息。

## <a name="span-idcommandringspanspan-idcommandringspanspan-idcommandringspancommand-ring"></a><span id="Command_Ring"></span><span id="command_ring"></span><span id="COMMAND_RING"></span>命令环


软件使用命令通道将命令传递到主控制器。 其中的某些命令定向到主控制器，以及一些将定向到特定的设备连接到主控制器。

## <a name="span-ideventringspanspan-ideventringspanspan-ideventringspanevent-ring"></a><span id="Event_Ring"></span><span id="event_ring"></span><span id="EVENT_RING"></span>事件环


主控制器使用事件环用于将事件传递到的软件。 也就是说，事件环是主机控制器用来通知操作已完成的驱动程序的结构。

## <a name="span-iddoorbellregisterarrayspanspan-iddoorbellregisterarrayspanspan-iddoorbellregisterarrayspandoorbell-register-array"></a><span id="Doorbell_Register_Array"></span><span id="doorbell_register_array"></span><span id="DOORBELL_REGISTER_ARRAY"></span>门铃注册数组


门铃注册数组是门铃寄存器中，一个用于每个设备连接到主控制器的数组。 1 到 255 之间的元素是门铃寄存器。 元素 0 指示命令环中是否存在挂起的命令。

软件通知主机控制器有与设备相关的或与终结点相关的工作，通过时，上下文信息写入到设备的门铃寄存器来执行。

下图将继续到上面的关系图的右侧。 它显示了表示单个终结点的其他数据结构。

![usb 3.0 数据结构显示终结点上下文具有多个 trbs 包含的数据和 tds](images/usb3structures02.png)

## <a name="span-idtransferringspanspan-idtransferringspanspan-idtransferringspantransfer-ring"></a><span id="Transfer_Ring"></span><span id="transfer_ring"></span><span id="TRANSFER_RING"></span>传输通道


每个终结点有一个或多个传输通道。 传输通道是传输请求的块 (TRBs) 的数组。 每个 TRB 指向连续数据块 (最多为 64 KB) 将硬件和内存中的作为一个单元之间传输的。

当 USB 3.0 核心堆栈从 USB 客户端驱动程序收到传输请求时，它传输时，标识终结点上下文，并传输请求然后拆分一个或多个传输描述符 (TDs)。 每个 t D 包含一个或多个 TRBs。

## <a name="span-idendpointcontextspanspan-idendpointcontextspanspan-idendpointcontextspanendpoint-context"></a><span id="Endpoint_Context"></span><span id="endpoint_context"></span><span id="ENDPOINT_CONTEXT"></span>终结点上下文


终结点上下文结构包含单个终结点的上下文信息。 它还具有**取消排队**并**排入队列**成员，用于跟踪位置 TRBs 已使用的硬件和软件还会添加 TRBs 的位置。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[USB 调试 Windows 8 中的创新](https://go.microsoft.com/fwlink/p/?LinkID=249153)

 

 






