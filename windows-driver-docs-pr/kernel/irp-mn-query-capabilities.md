---
title: IRP_MN_QUERY_CAPABILITIES
description: PnP 管理器将发送此 IRP，若要获取的设备，如是否已锁定或弹出设备的功能。函数和筛选器驱动程序可以处理此请求，如果他们更改总线驱动程序支持的功能。
ms.date: 08/12/2017
ms.assetid: 3c968a46-5bfb-4579-b09a-ad6bce4d9e3b
keywords:
- IRP_MN_QUERY_CAPABILITIES 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 3813da19b49203ccfa085b7ee8f12023e382e301
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576604"
---
# <a name="irpmnquerycapabilities"></a>IRP\_MN\_查询\_功能


PnP 管理器将发送此 IRP，若要获取的设备，如是否已锁定或弹出设备的功能。

函数和筛选器驱动程序可以处理此请求，如果他们更改总线驱动程序支持的功能。 总线驱动程序必须处理其子设备的此请求。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

立即后枚举设备时，即插即用管理器会将此 IRP 发送到设备的总线驱动程序。 设备的所有驱动程序具有启动设备后，即插即用管理器将再次发送此 IRP。 驱动程序可以发送此 IRP，若要获取设备的功能。

PnP 管理器和驱动程序在 IRQL 被动发送此 IRP\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.DeviceCapabilities.Capabilities**的成员[ **IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)结构指向[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)结构，它包含的功能的设备的信息。

## <a name="output-parameters"></a>输出参数


**Parameters.DeviceCapabilities.Capabilities**指向**设备\_功能**结构，它反映了由处理 IRP 的驱动程序进行任何修改。

## <a name="io-status-block"></a>I/O 状态块


驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态，例如状态\_未成功。

如果函数或筛选器驱动程序不处理此 IRP，则会调用[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355) ，并将传递到下一步的驱动程序 IRP。 此类驱动程序不能修改**Irp-&gt;IoStatus.Status** ，必须完成 IRP。

总线驱动程序设置**Irp-&gt;IoStatus.Status**并完成 IRP。

<a name="operation"></a>操作
---------

当枚举设备时，但为该设备加载的函数和筛选器驱动程序之前，即插即用管理器将发送**IRP\_MN\_查询\_功能**请求到的父总线驱动程序设备。 总线驱动程序必须设置相关的任何值[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)结构，并将其返回到 PnP 管理器。

构建设备堆栈和驱动程序已启动设备后，即插即用管理器将发送此 IRP 再次以按设备堆栈顶部的驱动程序，然后按堆栈中每个较低的驱动程序第一次处理。 函数和筛选器驱动程序可以设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程和手此 IRP 备份设备堆栈的句柄。

驱动程序将 IRP 传递到下一个较低的驱动程序之前应添加功能。

驱动程序应删除 IRP 用完所有较低的驱动程序的功能。 驱动程序通常不删除已由其他驱动程序设置的功能，但如果它在某些配置中具有特殊的功能的设备的信息可能会进行截断。 请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)推迟处理 IRP，直到完成较低的驱动程序有关的信息。

枚举设备以及将其驱动程序加载后，不应更改其功能。 如果设备已删除并重新枚举，可能会更改设备的功能。

在处理时**IRP\_MN\_查询\_功能**IRP，是设备的电源策略管理器的驱动程序应设置*IoCompletion*例程和复制设备电源功能，例如 S-D 电源状态映射 IRP 的方式重新启动设备堆栈上。 若要确定子设备的电源功能，父总线驱动程序创建另一个查询功能 IRP，并将 IRP 发送到其父驱动程序。 请参阅[报告设备电源功能](https://msdn.microsoft.com/library/windows/hardware/ff561058)有关详细信息。

如果驱动程序处理此 IRP，其应签**设备\_功能****版本**值。 如果该值不是该驱动程序支持的版本，该驱动程序失败，IRP。 如果支持该版本，该驱动程序应检查**大小**字段。 驱动程序应设置所收到作为输入的功能结构的边界内的字段。

处理此 IRP 的驱动程序可以设置一些**设备\_功能**字段，但不能设置**大小**并**版本**字段。 这些字段只能通过发送 IRP 的组件设置。

请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)处理的常规规则[即插即用次要 Irp](plug-and-play-minor-irps.md)。

**发送此 IRP**

总线驱动程序将此 IRP 发送到父设备堆栈时它处理**IRP\_MN\_查询\_功能**请求其子设备之一。 此外，驱动程序可能会发送此 IRP，若要获得其设备的设备功能。 单个驱动程序堆栈中的有一部分设备; 功能信息将 IRP 发送到设备堆栈启用它收集完整的图片，包括修改的任何筛选器驱动程序等。

请参阅[处理 Irp](https://msdn.microsoft.com/library/windows/hardware/ff546847)有关发送 Irp 信息。 专门针对此 IRP 可以采用以下步骤：

-   分配[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)结构从页面缓冲池，并将其初始化为零，通过调用[ **RtlZeroMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff563610). 初始化**大小**到**sizeof**(**设备\_功能**)，则**版本**为 1，和**地址**并**UINumber**为-1。

-   IRP 的下一步 I/O 堆栈位置中设置的值： 设置**MajorFunction**到[ **IRP\_MJ\_PNP**](irp-mj-pnp.md)，将**MinorFunction**到**IRP\_MN\_查询\_功能**，并设置**Parameters.DeviceCapabilities**为指针分配**设备\_功能**结构。

-   初始化**IoStatus.Status**于状态\_不\_受支持。

-   解除分配 IRP 和**设备\_功能**结构，在不再需要时。

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


[**DEVICE\_CAPABILITIES**](https://msdn.microsoft.com/library/windows/hardware/ff543095)

 

 




