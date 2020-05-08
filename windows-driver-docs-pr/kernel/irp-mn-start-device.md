---
title: IRP_MN_START_DEVICE
description: 所有 PnP 驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 0aac1346-b5c7-4dcc-ab86-03e8fd151505
keywords:
- IRP_MN_START_DEVICE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 5c461c2e52b1c6a37bc079a9114a5761bcc78ba2
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922517"
---
# <a name="irp_mn_start_device"></a>IRP\_MN\_启动\_设备


所有 PnP 驱动程序都必须处理此 IRP。

## <a name="value"></a>值

0x00

<a name="major-code"></a>主要代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

PnP 管理器会在向设备分配硬件资源（如果有）后发送此 IRP。 设备最近可能已枚举，并且是第一次启动，或者在停止资源重新平衡后，设备可能会重新启动。

有时，PnP 管理器会**将\_IRP\_MN\_START 设备**发送到已启动的设备，并提供一组不同于当前正在使用的设备的资源。 驱动程序通过以下方式启动此操作：调用[**IoInvalidateDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)并响应[**后续\_IRP\_MN\_QUERY\_PNP\_设备状态**](irp-mn-query-pnp-device-state.md)请求，并\_提供\_PNP\_资源要求更改标志集。 例如，总线驱动程序可以使用这种机制在 PCI 到 PCI bridge 上打开新的口径。

PnP 管理器在系统线程的上下文中\_以 IRQL 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的**StartDevice. AllocatedResources**成员指向一个[**CM\_\_资源列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)，描述 PnP 管理器分配给设备的硬件资源。 此列表包含原始格式的资源。 使用原始资源对设备进行编程。

**StartDevice. AllocatedResourcesTranslated**指向[**\_\_CM 资源列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)，描述 PnP 管理器分配给设备的硬件资源。 此列表包含以翻译形式列出的资源。 使用已翻译的资源连接中断向量、映射 i/o 空间和映射内存。

## <a name="output-parameters"></a>输出参数


None

## <a name="io-status-block"></a>I/o 状态块


驱动程序将**Irp-&gt;IOSTATUS**设置为状态\_"成功"，或设置为适当的错误状态\_，如 "\_状态\_不成功" 或 "状态资源不足"。

如果驱动程序需要一段时间才能对设备运行其启动操作，则可以将 IRP 标记为 "挂起"\_并返回 "挂起" 状态。

<a name="operation"></a>操作
---------

此 IRP 必须首先由设备的父总线驱动程序处理，然后由设备堆栈中的每个更高的驱动程序处理。

为了响应此 IRP，驱动程序将首次启动设备或重新启动已停止的设备。 启动设备所需的具体操作因设备而异，但可能包括打开设备、执行特定于设备的初始化以及连接中断。

驱动程序通常可以处理此 IRP，这与它是第一次启动设备还是在[**IRP\_\_MN 停止\_设备**](irp-mn-stop-device.md)之后重新启动设备（如果驱动程序在停止后重新启动时需要还原设备状态除外）。

在 Windows Vista 和更高版本的操作系统上，建议驱动程序始终**挂起\_IRP\_MN\_START DEVICE** IRP 并在以后完成其处理。 此顺序使系统可以异步处理设备重新启动。 （在 Windows Vista 之前的操作系统上，驱动程序可能\_会从其调度例程返回 "挂起" 状态，但 PnP 管理器不会与任何其他操作重叠设备重新启动。）

有关处理开始 IRP 的详细信息，请参阅[启动设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/starting-a-device)。

**正在发送此 IRP**

预留给系统使用。 驱动程序不得发送此 IRP。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IRP\_MN\_停止\_设备**](irp-mn-stop-device.md)

 

 




