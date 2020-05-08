---
title: IRP_MN_WRITE_CONFIG
description: 具有配置空间的总线的总线驱动程序必须为其子设备处理此请求（子 PDOs）。 函数和筛选器驱动程序不处理此请求。
ms.date: 08/12/2017
ms.assetid: d57c30b8-83bd-41c9-906d-b8c95f8ca54e
keywords:
- IRP_MN_WRITE_CONFIG 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 2070ed7b0927da2d230924921af17aa5edb54361
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922550"
---
# <a name="irp_mn_write_config"></a>IRP\_MN\_写入\_配置


具有配置空间的总线的总线驱动程序必须为其子设备处理此请求（子 PDOs）。 函数和筛选器驱动程序不处理此请求。

## <a name="value"></a>值

0x10

<a name="major-code"></a>主要代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

驱动程序或其他系统组件发送此 IRP，以将数据写入设备的父总线的配置空间。

驱动程序或其他系统组件在任意线程上下文中&lt;以\_IRQL 调度级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


**ReadWriteConfig**是包含以下信息的结构：

```cpp
ULONG WhichSpace;
PVOID Buffer;
ULONG Offset;
ULONG Length
```

不同的总线驱动程序可以采用不同的方式解释结构成员，但成员通常定义如下：

<a href="" id="whichspace"></a>**WhichSpace**  
指定配置空间。 有关可以为**WhichSpace**指定的值的信息，请参阅[**IRP\_MN\_READ\_CONFIG**](irp-mn-read-config.md)。

<a href="" id="buffer"></a>**宽限**  
指向包含要写入的数据的缓冲区。 缓冲区的格式是特定于总线的。

<a href="" id="offset"></a>**抵销**  
指定配置空间的偏移量。

<a href="" id="length"></a>**长短**  
指定要写入的字节数。

## <a name="output-parameters"></a>输出参数


在 i/o 状态块中返回。

## <a name="io-status-block"></a>I/o 状态块


总线驱动程序将**Irp-&gt;IoStatus**设置为状态\_成功，或设置为适当的错误状态，如\_状态\_无效的参数\_*n*、\_状态\_\_"没有此类设备\_"\_或 "状态\_设备未就绪"。

成功时，总线驱动程序会将**Irp&gt;-IoStatus**设置为写入的字节数。

如果总线驱动程序无法立即完成此请求，它可以将 IRP 标记为 "挂起"，返回\_状态 "挂起"，并在以后完成 IRP。

<a name="operation"></a>操作
---------

总线驱动程序为其子设备处理此 IRP （子 PDOs）。

函数和筛选器驱动程序不处理此 IRP;它们将其传递到下一个较低的驱动程序，而不会更改**&gt;IoStatus** ，并且不会设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程。

请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)，了解用于处理[即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

**正在发送此 IRP**

通常，函数驱动程序将此 IRP 发送到它所附加到的设备堆栈，并且 IRP 由父总线驱动程序进行处理。

有关发送 Irp 的信息，请参阅[处理 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps) 。 以下步骤专门适用于此 IRP：

-   从分页池分配一个缓冲区，并使用要写入的数据对其进行初始化。

-   在 IRP 的下一个 i/o 堆栈位置设置值：将**MajorFunction**设置为[**\_Irp\_MJ PNP**](irp-mj-pnp.md)，将**MinorFunction**设置为**\_irp MN\_写入\_CONFIG**，并在**ReadWriteConfig**中设置相应的值。

-   将**IoStatus**初始化为不\_受\_支持的状态。

-   如果不再需要 IRP 和缓冲区，请将其解除分配。

驱动程序必须从 IRQL &lt;调度\_级别发送此 IRP。

如果父总线驱动程序导出此类接口，则\_驱动程序可以通过总线接口例程在调度级别访问总线的配置空间。 为了获取总线接口，驱动程序会将[**IRP\_\_MN 查询\_接口**](irp-mn-query-interface.md)请求发送到其父总线驱动程序。 然后，驱动程序调用在接口中返回的相应例程。

例如，若要从\_调度级别写入配置空间，驱动程序可以在驱动程序初始化期间调用**IRP\_MN\_查询\_接口**，以便从父总线驱动程序获取[**总线\_接口\_标准**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard)接口。 驱动程序将查询 IRP 从 IRQL 被动\_级别发送。 稍后，从 IRQL 调度\_级别的代码，驱动程序调用在接口中返回的相应例程，如**SetBusData**例程。

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


[**IRP\_MN\_查询\_接口**](irp-mn-query-interface.md)

[**IRP\_MN\_读取\_配置**](irp-mn-read-config.md)

 

 




