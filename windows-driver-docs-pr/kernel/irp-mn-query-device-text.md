---
title: IRP_MN_QUERY_DEVICE_TEXT
description: PnP 管理器使用此 IRP 获取设备的说明或位置信息。如果总线支持此信息，则总线驱动程序必须为其子设备处理此请求。 函数和筛选器驱动程序不处理此 IRP。
ms.date: 08/12/2017
keywords:
- IRP_MN_QUERY_DEVICE_TEXT Kernel-Mode 驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 940b6e46231f1a0badb92da313b575acce7dc29b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827611"
---
# <a name="irp_mn_query_device_text"></a>IRP \_ MN \_ 查询 \_ 设备 \_ 文本


PnP 管理器使用此 IRP 获取设备的说明或位置信息。

如果总线支持此信息，则总线驱动程序必须为其子设备处理此请求。 函数和筛选器驱动程序不处理此 IRP。

## <a name="value"></a>“值”

0x0C

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

在枚举设备时，PnP 管理器将发送两个 Irp：一个用于查询设备说明，另一个用于查询位置信息。

PnP 管理器在 \_ 任意线程上下文中以 IRQL 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的 **QueryDeviceText. DeviceTextType** 成员是一个 **设备 \_ 文本 \_ 类型** 值，指定请求的字符串。 **设备 \_ 文本 \_ 类型** 的可能值包括 **DeviceTextDescription** 和 **DeviceTextLocationInformation**。

**QueryDeviceText** 是指定所请求文本区域设置的 LCID。

## <a name="output-parameters"></a>输出参数


在 i/o 状态块中返回。

## <a name="io-status-block"></a>I/o 状态块


驱动程序将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功" 或相应的 "错误" 状态。

成功时，总线驱动程序会将 **Irp &gt; IoStatus** 设置为指向驱动程序分配的内存块的指针，该内存块包含带有请求信息的 WCHAR 缓冲区。 出现错误时，总线驱动程序将 **Irp- &gt; IoStatus** 设置为零。

<a name="operation"></a>操作
---------

强烈建议总线驱动程序返回其子设备的设备说明。 如果未找到设备的 INF 匹配项，则会在 " **发现新硬件** " 弹出窗口中显示此字符串。

还鼓励总线驱动程序为其子设备返回 **LocationInformation** ，但此信息是可选的。 此字符串的格式取决于总线。 设备管理器会在设备的 "常规属性" 选项卡中显示此字符串。 供应商应选择向用户和支持人员传达有用信息的字符串。 例如，对于 PCI，字符串包含总线、设备和函数。 对于 PC 卡，字符串包含槽。

如果总线驱动程序返回信息以响应此 IRP，则会从分页内存中分配以 NULL 结尾的 Unicode 字符串。 当不再需要该字符串时，PnP 管理器将释放该字符串。

如果设备未提供说明或位置信息，则设备的父总线驱动程序完成 IRP ([**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) ，而不修改 **irp- &gt; IoStatus** 或 **irp- &gt; IoStatus**。

函数和筛选器驱动程序不处理此 IRP;它们将其传递到下一个较低的驱动程序，并且不会更改 **&gt; IoStatus**。

支持不同区域设置的不同文本字符串的总线驱动程序应能够处理设备未显式支持的语言的请求。 在这种情况下，总线驱动程序应返回与区域设置最接近的匹配项，或者应回退并返回某些合适的受支持的区域设置字符串。

请参阅 [即插即用](./introduction-to-plug-and-play.md) ，了解用于处理 [即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

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

 

