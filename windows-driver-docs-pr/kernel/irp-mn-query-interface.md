---
title: IRP_MN_QUERY_INTERFACE
description: IRP_MN_QUERY_INTERFACE 请求实现驱动程序将直接调用接口导出到其他驱动程序。导出接口的总线驱动程序必须处理其子设备 (子 PDOs) 的此请求。
ms.date: 08/12/2017
ms.assetid: ae1dab46-c387-4e5f-9368-451e625ddbc1
keywords:
- IRP_MN_QUERY_INTERFACE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 072b9a08d229a83ecf51833888d9394ab83c5500
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370855"
---
# <a name="irpmnqueryinterface"></a>IRP\_MN\_查询\_接口


**IRP\_MN\_查询\_接口**请求使驱动程序将直接调用接口导出到其他驱动程序。

导出接口的总线驱动程序必须处理其子设备 (子 PDOs) 的此请求。 函数和筛选器可以根据需要处理此请求。

"接口"在此上下文中的包含一个或多个例程和可能是由驱动程序或驱动程序集导出的数据。 接口具有描述其内容并标识其类型的 GUID 的结构。

例如，PCMCIA 总线驱动程序导出的接口的类型为 GUID\_PCMCIA\_接口\_标准，其中包含的操作，如获取 PCMCIA 内存卡的写保护条件例程。 此类内存卡功能驱动程序可以发送**IRP\_MN\_查询\_接口**到父 PCMCIA 总线驱动程序请求获取 PCMCIA 接口例程的指针。

本部分介绍查询界面 IRP 作为常规机制。 公开接口的驱动程序应提供有关其特定的接口的其他信息。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

驱动程序或系统组件发送此 IRP，若要获取有关导出的设备的驱动程序的接口的信息。

驱动程序或系统组件将此 IRP 发送在 IRQL = 被动\_级别在任意线程上下文中。

驱动程序的驱动程序后随时可以接收此 IRP [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程名为的设备。 设备可能会或可能发送此 IRP 时启动 (即，不能假定该驱动程序已成功完成[ **IRP\_MN\_启动\_设备**](irp-mn-start-device.md)设备的请求)。

## <a name="input-parameters"></a>输入参数


**Parameters.QueryInterface**的成员[ **IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)结构本身就是一种结构，用于描述所请求的接口。 该结构包含以下信息：

```cpp
CONST GUID *InterfaceType;
USHORT Size;
USHORT Version;
PINTERFACE Interface;
PVOID InterfaceSpecificData
```

结构的成员的定义，如下所示：

<a href="" id="interfacetype"></a>**InterfaceType**  
指向以标识所请求的接口的 GUID。 GUID 可以是系统定义的接口，如 GUID\_总线\_接口\_标准或自定义的接口。 Wdmguid.h 中列出了系统定义的接口的 Guid。 应使用 Uuidgen 生成自定义接口的 Guid。

<a href="" id="size"></a>**大小**  
指定所请求的接口的大小。 处理此 IRP 的驱动程序不能返回[**界面**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)结构大于**大小**字节。

<a href="" id="version"></a>**版本**  
指定所请求的接口的版本。

如果驱动程序支持多个接口的版本，该驱动程序返回最接近的受支持的版本不超出所请求的版本。 应检查返回的组件的发送 IRP **Interface.Version**字段，并确定要执行的操作根据该值。

<a href="" id="interface"></a>**接口**  
指向用于返回所请求的接口中的结构。 此结构必须包含[**界面**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)结构作为其第一个成员。 发送 IRP 的组件从分页的内存中分配此结构。

导出接口的驱动程序定义一个新的结构类型包含**接口**结构，外加的例程和/或界面中的数据成员。 (该驱动程序还定义接口的 GUID，如中所述**InterfaceType**成员、 更高版本。)

导出接口的驱动程序定义接口，包括从该处可以调用该例程，IRQL 等中的每个例程的执行环境。

<a href="" id="interfacespecificdata"></a>**InterfaceSpecificData**  
指定有关所请求的接口的其他信息。

对于某些界面中，发送 IRP 的组件在此字段中指定的其他信息。 通常情况下，此字段才**NULL**并**InterfaceType**并**版本**足以标识所请求的接口。

## <a name="output-parameters"></a>输出参数


如果成功，驱动程序填充中的成员**Parameters.QueryInterface.Interface**结构。

## <a name="io-status-block"></a>I/O 状态块


驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态。

如果成功，总线驱动程序设置**Irp-&gt;IoStatus.Information**为零。

如果函数或筛选器驱动程序不处理此 IRP，则会调用[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) ，并将传递到下一步的驱动程序 IRP。 此类驱动程序不能修改**Irp-&gt;IoStatus.Status** ，必须完成 IRP。

如果总线驱动程序不会导出所请求的接口，因此不处理此 IRP 子 PDO 总线驱动程序将离开**Irp-&gt;IoStatus.Status**完成 IRP 和时。

<a name="operation"></a>操作
---------

如果参数指定的接口，驱动程序支持将驱动程序处理此 IRP。

驱动程序必须排队此 IRP，如果 IRP 请求驱动程序不支持的接口。 驱动程序必须检查**Parameters.QueryInterface.InterfaceType**在其[ **IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)结构。 如果该接口不是一种驱动程序支持，该驱动程序必须通过 IRP 到设备堆栈中的下一个较低驱动程序而不会阻塞。

必须提供每个接口**InterfaceReference**并**InterfaceDereference**例程，并将导出接口的驱动程序必须提供在这些例程的地址[**接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)结构。 驱动程序到 IRP 的响应中返回的接口之前，它必须递增接口的引用计数，通过调用其**InterfaceReference**例程。 该驱动程序使用它完成请求的接口的驱动程序后，必须通过调用接口的递减引用计数**InterfaceDereference**例程。

如果该驱动程序，用于发送 IRP (驱动程序*x*) 更高版本将接口传递给另一个驱动程序 (驱动程序*y*) 然后驱动程序*x*必须递增接口的引用计数和驱动程序*y*必须使之减少。

处理此 IRP 的驱动程序应避免将 IRP 传递给另一个设备堆栈，以获取所请求的接口。 这样的设计将创建难以管理的设备堆栈之间的依赖关系。 例如，直到第一个堆栈中相应的驱动程序取消引用接口无法删除第二个设备堆栈所表示的设备。

接口可以是特定于总线的或总线无关。 这些总线的标头文件中定义特定于总线的接口。 系统定义独立于总线的接口， [**总线\_界面\_标准**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_bus_interface_standard)，用于导出标准总线接口。

请参阅[插](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)处理的常规规则[即插即用次要 Irp](plug-and-play-minor-irps.md)。

此 IRP 专门用于分层的内核模式设备驱动程序之间传递的例程的入口点。 不要混淆公开与此 IRP 的接口*设备接口*。 设备接口可供用户模式组件或其他内核组件主要用于公开到设备以供使用的路径。 有关设备接口的详细信息，请参阅[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)。

**发送此 IRP**

请参阅[处理 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)有关发送 Irp 信息。 专门针对此 IRP 可以采用以下步骤：

-   分配[**界面**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)结构从页面缓冲池并将其初始化为零。 如果该接口将调用在 IRQL &gt;= 调度\_级别，基于接口协定上，调用方可以将内容复制到从非分页缓冲池分配的内存。

-   IRP 的下一步 I/O 堆栈位置中设置的值： 设置**MajorFunction**到[ **IRP\_MJ\_PNP**](irp-mj-pnp.md)，将**MinorFunction**到**IRP\_MN\_查询\_接口**，并设置相应的值**Parameters.QueryInterface**。

-   初始化**IoStatus.Status**于状态\_不\_受支持。

-   解除分配 IRP 和**接口**结构，在不再需要时。

-   使用接口例程和上下文参数，如接口规范中所述。

-   递减引用计数使用[ *InterfaceDereference* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pinterface_dereference)例程时不再需要该接口。 请勿取消对接口的引用后调用任何接口例程。

驱动程序通常将此 IRP 发送到在其中附加驱动程序设备堆栈的顶部。 如果驱动程序将此 IRP 发送到不同的设备堆栈，驱动程序必须注册其他设备上的目标设备通知，如果另一台设备不是设备驱动程序正在处理的祖先。 此类驱动程序调用[ **IoRegisterPlugPlayNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterplugplaynotification)与*EventCategory*的**EventCategoryTargetDeviceChange**。 该驱动程序时接收通知的类型的 GUID\_目标\_设备\_查询\_删除，该驱动程序必须取消引用接口。 该驱动程序可以再次查询接口收到后续 GUID\_目标\_设备\_删除\_已取消通知。

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


[**总线\_接口\_标准**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_bus_interface_standard)

[**INTERFACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)

[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterplugplaynotification)

 

 




