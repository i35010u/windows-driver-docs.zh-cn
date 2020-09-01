---
title: IRP_MN_WRITE_CONFIG
description: 具有配置空间的总线的总线驱动程序必须为其子设备处理此请求 (子 PDOs) 。 函数和筛选器驱动程序不处理此请求。
ms.date: 08/12/2017
ms.assetid: d57c30b8-83bd-41c9-906d-b8c95f8ca54e
keywords:
- IRP_MN_WRITE_CONFIG 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: f354dd608d929982e28dbd0997c43a06cedbdb8d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189319"
---
# <a name="irp_mn_write_config"></a>IRP \_ MN \_ 写入 \_ 配置


具有配置空间的总线的总线驱动程序必须为其子设备处理此请求 (子 PDOs) 。 函数和筛选器驱动程序不处理此请求。

## <a name="value"></a>值

0x10

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

驱动程序或其他系统组件发送此 IRP，以将数据写入设备的父总线的配置空间。

驱动程序或其他系统组件 &lt; \_ 在任意线程上下文中以 IRQL 调度级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


**ReadWriteConfig** 是包含以下信息的结构：

```cpp
ULONG WhichSpace;
PVOID Buffer;
ULONG Offset;
ULONG Length
```

不同的总线驱动程序可以采用不同的方式解释结构成员，但成员通常定义如下：

<a href="" id="whichspace"></a>**WhichSpace**  
指定配置空间。 有关可以为 **WhichSpace**指定的值的信息，请参阅 [**IRP \_ MN \_ READ \_ CONFIG**](irp-mn-read-config.md)。

<a href="" id="buffer"></a>**宽限**  
指向包含要写入的数据的缓冲区。 缓冲区的格式是特定于总线的。

<a href="" id="offset"></a>**抵销**  
指定配置空间的偏移量。

<a href="" id="length"></a>**长短**  
指定要写入的字节数。

## <a name="output-parameters"></a>输出参数


在 i/o 状态块中返回。

## <a name="io-status-block"></a>I/o 状态块


总线驱动程序将**Irp- &gt; IoStatus**设置为状态 \_ 成功，或设置为适当的错误状态，如 \_ 状态 \_ 无效 \_ 的参数*n*、状态 " \_ 没有 \_ 此类 \_ 设备" 或 "状态 \_ 设备 \_ 未就绪" \_ 。

成功时，总线驱动程序会将 **Irp- &gt; IoStatus** 设置为写入的字节数。

如果总线驱动程序无法立即完成此请求，它可以将 IRP 标记为 "挂起"，返回状态 \_ "挂起"，并在以后完成 IRP。

<a name="operation"></a>操作
---------

总线驱动程序为其子设备处理此 IRP (子 PDOs) 。

函数和筛选器驱动程序不处理此 IRP;它们将其传递到下一个较低的驱动程序，而不会更改 ** &gt; IoStatus** ，并且不会设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程。

请参阅 [即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play) ，了解用于处理 [即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

**正在发送此 IRP**

通常，函数驱动程序将此 IRP 发送到它所附加到的设备堆栈，并且 IRP 由父总线驱动程序进行处理。

有关发送 Irp 的信息，请参阅 [处理 irp](./handling-irps.md) 。 以下步骤专门适用于此 IRP：

-   从分页池分配一个缓冲区，并使用要写入的数据对其进行初始化。

-   在 IRP 的下一个 i/o 堆栈位置设置值：将 **MajorFunction** 设置为 [**irp \_ MJ \_ PNP**](irp-mj-pnp.md)，将 **MinorFunction** 设置为 **irp \_ MN \_ 写入 \_ CONFIG**，并在 **ReadWriteConfig**中设置相应的值。

-   将 **IoStatus** 初始化为 \_ 不 \_ 受支持的状态。

-   如果不再需要 IRP 和缓冲区，请将其解除分配。

驱动程序必须从 IRQL 调度级别发送此 IRP &lt; \_ 。

\_如果父总线驱动程序导出此类接口，则驱动程序可以通过总线接口例程在调度级别访问总线的配置空间。 为了获取总线接口，驱动程序会将 [**IRP \_ MN \_ 查询 \_ 接口**](irp-mn-query-interface.md) 请求发送到其父总线驱动程序。 然后，驱动程序调用在接口中返回的相应例程。

例如，若要从调度级别写入配置空间， \_ 驱动程序可以在驱动程序初始化期间调用 **IRP \_ MN \_ 查询 \_ 接口** ，以便从父总线驱动程序获取 [**总线 \_ 接口 \_ 标准**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard) 接口。 驱动程序将查询 IRP 从 IRQL 被动 \_ 级别发送。 稍后，从 IRQL 调度级别的代码， \_ 驱动程序调用在接口中返回的相应例程，如 **SetBusData** 例程。

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
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**IRP \_ MN \_ 查询 \_ 接口**](irp-mn-query-interface.md)

[**IRP \_ MN \_ 读取 \_ 配置**](irp-mn-read-config.md)

 

