---
title: 将 AddDevice 移植到 EvtDriverDeviceAdd
description: 将 AddDevice 移植到 EvtDriverDeviceAdd
ms.assetid: 8FCFDA98-621E-415E-83D7-0371F55DD8A8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6eb9f685aebd3a65e4a8821737e8f1f016b3f1ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390103"
---
# <a name="porting-adddevice-to-evtdriverdeviceadd"></a>将 AddDevice 移植到 EvtDriverDeviceAdd


支持即插每个内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF) 驱动程序必须具有[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调，它可以正常运行的等效WDM 驱动程序[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)函数。

WDM [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)函数创建设备对象、 创建设备接口，并初始化 WMI 但还可以初始化设备驱动程序的扩展中的许多变量。 WDM 驱动程序通常延迟的 I/O 队列和中断的对象，直到创建[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)函数调用以处理[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求。

基于框架的驱动程序的[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调创建 WDFDEVICE 对象来表示的设备，只需枚举。 它还执行许多额外的初始化任务提供框架，它需要设置其自己的内部结构和基础 WDM 结构的信息。

因此，对于大多数基于框架的驱动程序[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调是比相应 WDM [ *AddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff540521)函数。 在基于框架的驱动程序，几乎所有的设备的初始化代码位于*EvtDriverDeviceAdd*函数。 但是，在 WDM 版本中，初始化代码往往分散通过驱动程序中的多个函数。

中的代码[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)按以下顺序出现：

1.  填写[WDFDEVICE\_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951)结构，它提供用于创建设备对象的信息。 详细了解使用 WDFDEVICE\_INIT，请参阅[创建 Framework 设备对象](creating-a-framework-device-object.md)。
2.  设置设备对象的上下文区域中，它类似于 WDM 设备扩展。
3.  [创建设备对象](creating-a-framework-device-object.md)。
4.  执行附加的初始化和启动任务，如[创建的 I/O 队列](creating-i-o-queues.md)并[中断对象](creating-an-interrupt-object.md)。

KMDF 总线驱动程序通常会创建多个设备对象： 作为总线本身的功能驱动程序的作用 FDO 和每个子设备连接到总线 PDO。 框架将调用的驱动程序[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)系统枚举总线时的功能。 然后，驱动程序本身枚举其子设备，并创建 PDOs 来表示它们。 同时支持 KMDF[静态](static-enumeration.md)并[动态](dynamic-enumeration.md)子设备枚举。 它还包括其他特定于 PDO 的功能。

## <a name="device-object-context-area"></a>设备对象上下文区域


驱动程序通常需要维护指针和对象特定于数据的设备对象与关联的存储。 WDM 驱动程序，在**DeviceExtension**字段[**设备\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff543147)结构提供了此类存储。 在基于框架的驱动程序，WDFDEVICE 对象的对象上下文区域的作用相同。

有关分配和访问 framework 对象的上下文空间的信息，请参阅[框架对象上下文空间](framework-object-context-space.md)。

## <a name="device-object-creation"></a>创建设备对象


WDM 驱动程序创建[**设备\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff543147)结构来表示每个设备对象并将设备对象附加到插设备堆栈。 基于框架的驱动程序还创建设备对象，通过使用 WDFDEVICE 句柄进行引用。

WDF 驱动程序将调用的所需的初始化方法后，它设置的设备对象的属性 (通常情况下，大小和类型的上下文区域)，然后调用[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)创建设备对象。 **WdfDeviceCreate**创建 WDFDEVICE 对象和基础 WDM [**设备\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff543147)，将附加 WDM**设备\_对象**到设备堆栈和返回的句柄 WDFDEVICE 对象。

## <a name="additional-evtdriverdeviceadd-tasks"></a>其他 EvtDriverDeviceAdd 任务


基于框架的驱动程序创建的设备对象后，它应当：

-   [创建的 I/O 队列](creating-i-o-queues.md)并指定[请求处理程序](request-handlers.md)设备对象。
-   [创建设备接口](using-device-interfaces.md)。
-   设置[设备空闲策略](supporting-idle-power-down.md)并[唤醒设置](supporting-system-wake-up.md)，如果设备对象拥有电源策略。
-   [创建一个中断对象](creating-an-interrupt-object.md)，如果硬件支持中断。
-   [初始化 WMI](supporting-wmi-in-kmdf-drivers.md)。<sup>†</sup>

† 此功能才是可用于 KMDF 驱动程序。

基于框架的驱动程序应设置 I/O 队列并创建中的中断对象[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调后立即创建设备对象。 框架连接中断对象，并在适当的时间更高版本，将队列启动的启动设备处理过程中。

## <a name="child-device-enumeration-pdos-kmdf-only"></a>子设备枚举 （PDOs，仅 KMDF）


通常控制总线驱动程序创建多个设备对象： 作为总线本身的功能驱动程序的作用 FDO 和每个子设备连接到总线 PDO。 KMDF 支持子设备的静态和动态枚举。 它还包括其他特定于 PDO 的功能。

框架调用的驱动程序[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)插 manager 枚举总线时的功能。 *EvtDriverDeviceAdd*创建 FDO 总线，然后枚举子设备并创建每个 PDO。 该驱动程序可以枚举子设备既[静态](static-enumeration.md)或[动态](dynamic-enumeration.md)。

某些回调函数仅适用于表示 PDOs 的设备对象。 该驱动程序初始化时的设备对象，它会注册相应的回调。 PDOs 响应有关设备的资源和资源要求，请求锁定或弹出设备时，查询和请求来启用和禁用设备唤醒信号。

在 WDM 驱动程序，这些请求到达次要 IRP 代码中作为[ **IRP\_MJ\_PNP** ](https://msdn.microsoft.com/library/windows/hardware/ff550772)或者[ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)请求。 KMDF 驱动程序处理它们的实现的回调和设备对象初始化期间通过调用注册回调[ **WdfPdoInitSetEventCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff548805)。 下表列出了特定于 PDO 的回调：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KMDF 回调</th>
<th align="left">WDM IRP</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540895" data-raw-source="[&lt;em&gt;EvtDeviceResourcesQuery&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540895)"><em>EvtDeviceResourcesQuery</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551710" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_RESOURCES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551710)"><strong>IRP_MN_QUERY_RESOURCES</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540894" data-raw-source="[&lt;em&gt;EvtDeviceResourceRequirementsQuery&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540894)"><em>EvtDeviceResourceRequirementsQuery</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551715" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_RESOURCE_REQUIREMENTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551715)"><strong>IRP_MN_QUERY_RESOURCE_REQUIREMENTS</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540863" data-raw-source="[&lt;em&gt;EvtDeviceEject&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540863)"><em>EvtDeviceEject</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550853" data-raw-source="[&lt;strong&gt;IRP_MN_EJECT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550853)"><strong>IRP_MN_EJECT</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540909" data-raw-source="[&lt;em&gt;EvtDeviceSetLock&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540909)"><em>EvtDeviceSetLock</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551742" data-raw-source="[&lt;strong&gt;IRP_MN_SET_LOCK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551742)"><strong>IRP_MN_SET_LOCK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540866" data-raw-source="[&lt;em&gt;EvtDeviceEnableWakeAtBus&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540866)"><em>EvtDeviceEnableWakeAtBus</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551766" data-raw-source="[&lt;strong&gt;IRP_MN_WAIT_WAKE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551766)"><strong>IRP_MN_WAIT_WAKE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540858" data-raw-source="[&lt;em&gt;EvtDeviceDisableWakeAtBus&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540858)"><em>EvtDeviceDisableWakeAtBus</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551766" data-raw-source="[&lt;strong&gt;IRP_MN_WAIT_WAKE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551766)"><strong>IRP_MN_WAIT_WAKE</strong></a></p></td>
</tr>
</tbody>
</table>

 

其他**WdfPdoInitXxx**方法启用要指定特定于设备的数据，例如设备 Id 的驱动程序。

 

 





