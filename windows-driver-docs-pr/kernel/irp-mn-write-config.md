---
title: IRP_MN_WRITE_CONFIG
description: 对于具有配置空间总线总线驱动程序必须处理其子设备 (子 PDOs) 的此请求。 函数和筛选器驱动程序不处理此请求。
ms.date: 08/12/2017
ms.assetid: d57c30b8-83bd-41c9-906d-b8c95f8ca54e
keywords:
- IRP_MN_WRITE_CONFIG 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: b12c949ad7a4ef2f3c56d242645d1aefb77d7176
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376454"
---
# <a name="irpmnwriteconfig"></a>IRP\_MN\_WRITE\_CONFIG


对于具有配置空间总线总线驱动程序必须处理其子设备 (子 PDOs) 的此请求。 函数和筛选器驱动程序不处理此请求。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

驱动程序或其他系统组件发送此 IRP 将数据写入到设备的父总线的配置空间。

驱动程序或其他系统组件将此 IRP 发送在 IRQL&lt;调度\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.ReadWriteConfig**是一种结构包含以下信息：

```cpp
ULONG WhichSpace;
PVOID Buffer;
ULONG Offset;
ULONG Length
```

结构的成员可以有不同的解释不同总线驱动程序，但成员通常定义，如下所示：

<a href="" id="whichspace"></a>**WhichSpace**  
指定的配置空间。 有关可以为指定的值信息**WhichSpace**，请参阅[ **IRP\_MN\_读取\_配置**](irp-mn-read-config.md)。

<a href="" id="buffer"></a>**缓冲区**  
指向包含要写入的数据的缓冲区。 缓冲区的格式是特定于总线的。

<a href="" id="offset"></a>**Offset**  
到配置空间指定偏移量。

<a href="" id="length"></a>**长度**  
指定要写入的字节数。

## <a name="output-parameters"></a>输出参数


返回在 I/O 状态块中。

## <a name="io-status-block"></a>I/O 状态块


总线驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态，例如状态\_无效\_参数\_*n*，状态\_否\_SUCH\_设备或状态\_设备\_不\_准备就绪。

如果成功，总线驱动程序设置**Irp-&gt;IoStatus.Information**到写入的字节数。

如果总线驱动程序不能立即完成此请求，它可以将挂起的 IRP 标记，则返回状态\_PENDING，并在以后完成 IRP。

<a name="operation"></a>操作
---------

总线驱动程序处理其子设备 (子 PDOs) 此 IRP。

函数和筛选器驱动程序不处理此 IRP;它们将其传递给下一个较低驱动程序和无变化**Irp-&gt;IoStatus.Status**并且未设置[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程。

请参阅[插](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)处理的常规规则[即插即用次要 Irp](plug-and-play-minor-irps.md)。

**发送此 IRP**

通常情况下，功能驱动程序将此 IRP 发送到设备堆栈向其附加并由父总线驱动程序处理 IRP。

请参阅[处理 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)有关发送 Irp 信息。 专门针对此 IRP 可以采用以下步骤：

-   分配来自分页池的缓冲区并将其初始化与要写入的数据。

-   IRP 的下一步 I/O 堆栈位置中设置的值： 设置**MajorFunction**到[ **IRP\_MJ\_PNP**](irp-mj-pnp.md)，将**MinorFunction**到**IRP\_MN\_编写\_CONFIG**，并设置相应的值**Parameters.ReadWriteConfig**。

-   初始化**IoStatus.Status**于状态\_不\_受支持。

-   在不再需要时，解除分配 IRP 和缓冲区。

驱动程序必须将此 IRP 发送从 IRQL&lt;调度\_级别。

驱动程序可以访问在调度的总线配置空间\_级别通过总线接口例程中，如果父总线驱动程序导出此类接口。 若要获取总线接口，驱动程序发送[ **IRP\_MN\_查询\_接口**](irp-mn-query-interface.md)请求到其父总线驱动程序。 然后，驱动程序调用在界面中返回的相应例程。

例如，若要配置空间编写从调度\_驱动程序可以调用的级别**IRP\_MN\_查询\_接口**若要获取的驱动程序初始化期间[**总线\_界面\_标准**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_bus_interface_standard)从父总线驱动程序的接口。 该驱动程序会将查询 IRP 发送从 IRQL 被动\_级别。 更高版本，从代码在 IRQL 调度\_级别，该驱动程序调用相应的例程返回在界面中，如**Interface.SetBusData**例程。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**IRP\_MN\_查询\_接口**](irp-mn-query-interface.md)

[**IRP\_MN\_READ\_CONFIG**](irp-mn-read-config.md)

 

 




