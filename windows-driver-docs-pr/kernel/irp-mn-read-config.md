---
title: IRP_MN_READ_CONFIG
description: 对于具有配置空间总线总线驱动程序必须处理其子设备 (子 PDOs) 的此请求。 筛选器和函数的驱动程序不处理此请求。
ms.date: 08/12/2017
ms.assetid: cbc5b959-0aae-4c86-b490-296965a7f158
keywords:
- IRP_MN_READ_CONFIG 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 3bb3a95a97e2de5a3c139b7485f9f930da15ec02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563025"
---
# <a name="irpmnreadconfig"></a>IRP\_MN\_READ\_CONFIG


对于具有配置空间总线总线驱动程序必须处理其子设备 (子 PDOs) 的此请求。 筛选器和函数的驱动程序不处理此请求。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

驱动程序或其他系统组件发送此 IRP 读取设备的父总线的配置空间。

驱动程序或其他系统组件将此 IRP 发送在 IRQL&lt;调度\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.ReadWriteConfig**的成员[ **IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)结构本身就是一个包含以下结构信息：

```cpp
ULONG WhichSpace;
PVOID Buffer;
ULONG Offset;
ULONG Length
```

结构的成员可以有不同的解释不同总线驱动程序，但成员通常定义，如下所示：

<a href="" id="whichspace"></a>**WhichSpace**  
指定要访问的内存区域。 此参数的取值可为：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>Bus</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PCI_WHICHSPACE_CONFIG</p></td>
<td><p>PCI</p></td>
<td><p>PCI 配置空间。</p></td>
</tr>
<tr class="even">
<td><p>PCI_WHICHSPACE_ROM</p></td>
<td><p>PCI</p></td>
<td><p>只读内存。</p></td>
</tr>
<tr class="odd">
<td><p>PCCARD_COMMON_MEMORY</p>
<p>PCCARD_COMMON_MEMORY_INDIRECT</p></td>
<td><p>PCMCIA</p></td>
<td><p>Main PCCARD 内存。</p></td>
</tr>
<tr class="even">
<td><p>PCCARD_ATTRIBUTE_MEMORY</p>
<p>PCCARD_ATTRIBUTE_MEMORY_INDIRECT</p></td>
<td><p>PCMCIA</p></td>
<td><p>PCMCIA 属性 （配置） 空间。</p></td>
</tr>
<tr class="odd">
<td><p>PCCARD_PCI_CONFIGURATION_SPACE</p></td>
<td><p>PCMCIA</p></td>
<td><p>PCI 配置空间。</p></td>
</tr>
</tbody>
</table>

 

PCI\_*XXX*中 wdm.h 中定义了值。 PCCARD\_*XXX* Ntddpcm.h 中定义了值。

<a href="" id="buffer"></a>**缓冲区**  
指向用于返回所请求的信息的缓冲区。 发送 IRP 的组件从分页的内存中分配此结构。 缓冲区的格式是特定于总线的。

<a href="" id="offset"></a>**Offset**  
到配置空间指定偏移量。

<a href="" id="length"></a>**长度**  
指定要读取的字节数。

## <a name="output-parameters"></a>输出参数


如果成功，总线驱动程序填充缓冲区**Parameters.ReadWriteConfig.Buffer**与所请求的数据。

## <a name="io-status-block"></a>I/O 状态块


总线驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态，例如状态\_无效\_参数\_*n*，状态\_否\_SUCH\_设备或状态\_设备\_不\_准备就绪。

如果成功，总线驱动程序设置**Irp-&gt;IoStatus.Information**返回到的字节数。

如果无法完成此请求，它可以将标记挂起的 IRP 立即总线驱动程序，将返回状态\_PENDING，并在以后完成 IRP。

<a name="operation"></a>操作
---------

总线驱动程序处理其子设备 (子 PDOs) 此 IRP。

函数和筛选器驱动程序不处理此 IRP;它们将其传递给下一个较低驱动程序和无变化**Irp-&gt;IoStatus**。未设置状态和它们[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程。

处理此请求的总线驱动程序应检查 WhichSpace 参数以确保它包含一个值，该驱动程序支持该值。

请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)处理的常规规则[即插即用次要 Irp](plug-and-play-minor-irps.md)。

**发送此 IRP**

通常情况下，功能驱动程序将此 IRP 发送到设备堆栈向其附加并由父总线驱动程序处理 IRP 中的顶部驱动程序。

请参阅[处理 Irp](https://msdn.microsoft.com/library/windows/hardware/ff546847)有关发送 Irp 信息。 专门针对此 IRP 可以采用以下步骤：

-   分配来自分页池的缓冲区并将其初始化为零。

-   IRP 的下一步 I/O 堆栈位置中设置的值： 设置**MajorFunction**到[ **IRP\_MJ\_PNP**](irp-mj-pnp.md)，将**MinorFunction**到**IRP\_MN\_读取\_CONFIG**，并设置相应的值**Parameters.ReadWriteConfig**。

-   初始化**IoStatus.Status**于状态\_不\_受支持。

-   在不再需要时，解除分配 IRP 和缓冲区。

驱动程序必须将此 IRP 发送从 IRQL&lt;调度\_级别。

驱动程序可以访问在调度的总线配置空间\_级别通过总线接口例程中，如果父总线驱动程序支持此类的接口。 若要获取总线接口，驱动程序发送[ **IRP\_MN\_查询\_接口**](irp-mn-query-interface.md)设备堆栈中的附加驱动程序的请求。 然后，驱动程序调用在界面中返回的相应例程。

例如，若要配置空间读取调度\_级别，驱动程序可以调用**IRP\_MN\_查询\_接口**若要获取的驱动程序初始化期间[**总线\_界面\_标准**](https://msdn.microsoft.com/library/windows/hardware/ff540707)从父总线驱动程序的接口。 该驱动程序会将查询 IRP 发送从 IRQL 被动\_级别。 更高版本，从代码在 IRQL 调度\_级别，该驱动程序调用相应的例程返回在界面中，如**Interface.GetBusData**例程。

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

[**IRP\_MN\_WRITE\_CONFIG**](irp-mn-write-config.md)

 

 




