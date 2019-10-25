---
title: IRP_MN_START_DEVICE
description: 所有 PnP 驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 0aac1346-b5c7-4dcc-ab86-03e8fd151505
keywords:
- IRP_MN_START_DEVICE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 23ca09dabcc2000a75662db4a632a0ffc3908cb9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827945"
---
# <a name="irp_mn_start_device"></a>IRP\_MN\_启动\_设备


所有 PnP 驱动程序都必须处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)发送时间
---------

PnP 管理器会在向设备分配硬件资源（如果有）后发送此 IRP。 设备最近可能已枚举，并且是第一次启动，或者在停止资源重新平衡后，设备可能会重新启动。

有时，PnP 管理器会将**IRP\_MN\_启动\_设备**发送到已启动的设备，并提供一组与当前使用的设备不同的资源。 驱动程序通过以下方式启动此操作：调用[**IoInvalidateDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)并响应后续[**IRP\_MN\_QUERY\_pnp\_设备\_状态**](irp-mn-query-pnp-device-state.md)请求与 pnp\_资源\_要求\_更改标志集。 例如，总线驱动程序可以使用这种机制在 PCI 到 PCI bridge 上打开新的口径。

PnP 管理器以 IRQL 被动\_级别在系统线程的上下文中发送此 IRP。

## <a name="input-parameters"></a>输入参数


[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的**StartDevice. AllocatedResources**成员指向[**CM\_资源\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)，该列表描述 PnP 管理器分配到的硬件资源。装置. 此列表包含原始格式的资源。 使用原始资源对设备进行编程。

**StartDevice. AllocatedResourcesTranslated**指向[**CM\_资源\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)，描述 PnP 管理器分配给设备的硬件资源。 此列表包含以翻译形式列出的资源。 使用已翻译的资源连接中断向量、映射 i/o 空间和映射内存。

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/O 状态块


驱动程序将**Irp&gt;IoStatus**的状态设置为 "状态"\_成功，或设置为适当的错误状态，如状态\_"未成功" 或 "状态"\_"\_资源不足"。

如果驱动程序需要一段时间才能对设备运行其启动操作，则可以将 IRP 标记为 "挂起" 并返回状态\_"挂起"。

<a name="operation"></a>操作
---------

此 IRP 必须首先由设备的父总线驱动程序处理，然后由设备堆栈中的每个更高的驱动程序处理。

为了响应此 IRP，驱动程序将首次启动设备或重新启动已停止的设备。 启动设备所需的具体操作因设备而异，但可能包括打开设备、执行特定于设备的初始化以及连接中断。

通常，驱动程序可以采用与在[**irp\_MN\_停止\_设备**](irp-mn-stop-device.md)后第一次启动设备或重新启动设备之后启动设备相同的方式来处理此 IRP，但当驱动程序在停止后重新启动时，驱动程序是否需要还原设备状态。

在 Windows Vista 和更高版本的操作系统上，建议驱动程序始终挂起**IRP\_MN\_启动\_设备**IRP 并在以后完成其处理。 此顺序使系统可以异步处理设备重新启动。 （在 Windows Vista 之前的操作系统上，驱动程序可能会从其调度例程返回状态\_"挂起"，但 PnP 管理器不会将设备重新启动与任何其他操作重叠。）

有关处理开始 IRP 的详细信息，请参阅[启动设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/starting-a-device)。

**正在发送此 IRP**

保留供系统使用。 驱动程序不得发送此 IRP。

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
<td>Wdm .h （包括 Wdm、Ntddk 或 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IRP\_MN\_停止\_设备**](irp-mn-stop-device.md)

 

 




