---
title: 将 AddDevice 移植到 EvtDriverDeviceAdd
description: 将 AddDevice 移植到 EvtDriverDeviceAdd
ms.assetid: 8FCFDA98-621E-415E-83D7-0371F55DD8A8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 197d4334471d6e8bbab2c034eebbe091fccb2646
ms.sourcegitcommit: 057b72e8a44ba8f4282e072edc7be0b7e9341d2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89412470"
---
# <a name="porting-adddevice-to-evtdriverdeviceadd"></a>将 AddDevice 移植到 EvtDriverDeviceAdd


支持即插即用的每个内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF) 驱动程序必须具有 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调，该回调等效于 WDM 驱动程序的 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 函数。

WDM [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 函数创建设备对象，创建设备接口，并初始化 WMI，还在驱动程序的设备扩展中初始化大量变量。 WDM 驱动程序通常会在调用 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 函数来处理 [**IRP \_ MN \_ 启动 \_ 设备**](../kernel/irp-mn-start-device.md) 请求之前，延迟创建 i/o 队列和中断对象。

基于框架的驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调创建 WDFDEVICE 对象，用于表示刚刚枚举的设备。 它还执行许多额外的初始化任务，为框架提供设置自己的内部结构和基础 WDM 结构所需的信息。

因此，对于大多数基于框架的驱动程序， [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调比相应的 WDM [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 函数要长得多。 在基于框架的驱动程序中，几乎所有设备的初始化代码都在 *EvtDriverDeviceAdd* 函数中。 但是，在 WDM 版本中，初始化代码通常会通过驱动程序中的多个函数进行分布。

[*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)中的代码按以下顺序显示：

1.  填写 [WDFDEVICE \_ INIT](./wdfdevice_init.md) 结构，它提供用于创建设备对象的信息。 有关使用 WDFDEVICE INIT 的详细信息 \_ ，请参阅 [创建框架设备对象](creating-a-framework-device-object.md)。
2.  设置设备对象的上下文区域，这与 WDM 设备扩展类似。
3.  [创建设备对象](creating-a-framework-device-object.md)。
4.  执行其他初始化和启动任务，如 [创建 i/o 队列](creating-i-o-queues.md) 和 [中断对象](creating-an-interrupt-object.md)。

KMDF 总线驱动程序通常会创建多个设备对象：其角色的 FDO 作为总线本身的函数驱动程序，以及连接到总线的每个子设备的 PDO。 当系统枚举总线时，框架将调用驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 函数。 然后，驱动程序本身枚举其子设备并创建 PDOs 来表示它们。 KMDF 支持子设备的 [静态](static-enumeration.md) 和 [动态](dynamic-enumeration.md) 枚举。 它还包括其他特定于 PDO 的功能。

## <a name="device-object-context-area"></a>设备对象上下文区域


驱动程序通常需要与设备对象相关联的存储来维护指针和特定于对象的数据。 在 WDM 驱动程序中，[**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构的 " **DeviceExtension** " 字段提供了此类存储。 在基于框架的驱动程序中，WDFDEVICE 对象的对象上下文区域可实现相同的目的。

有关为框架对象分配和访问上下文空间的信息，请参阅 [框架对象上下文空间](framework-object-context-space.md)。

## <a name="device-object-creation"></a>设备对象创建


WDM 驱动程序创建 [**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object) 结构来表示每个设备对象，并将设备对象附加到即插即用设备堆栈。 基于框架的驱动程序还会创建设备对象，这些对象通过使用 WDFDEVICE 句柄来引用。

在 WDF 驱动程序调用所需的初始化方法后，它会为设备对象设置特性 (通常是上下文区域的大小和类型) 然后调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 创建设备对象。 **WdfDeviceCreate**创建 WDFDEVICE 对象和基础 WDM 设备对象，将 WDM**设备 \_ 对象**附加到设备堆栈，并返回 WDFDEVICE 对象的句柄。 [** \_ **](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)

## <a name="additional-evtdriverdeviceadd-tasks"></a>其他 EvtDriverDeviceAdd 任务


在基于框架的驱动程序创建设备对象之后，应执行以下操作：

-   [创建 i/o 队列](creating-i-o-queues.md) 并为设备对象指定 [请求处理程序](request-handlers.md) 。
-   [创建设备接口](using-device-interfaces.md)。
-   如果设备对象拥有电源策略，请设置 [设备空闲策略](supporting-idle-power-down.md) 和 [唤醒设置](supporting-system-wake-up.md)。
-   如果硬件支持中断，则[创建一个中断对象](creating-an-interrupt-object.md)。
-   [初始化 WMI](introduction-to-wmi-for-kmdf-drivers.md)。<sup>†</sup>

†此功能仅适用于 KMDF 驱动程序。

基于框架的驱动程序应设置 i/o 队列，并在创建设备对象之后立即在 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调中创建中断对象。 在开始设备处理期间，框架将连接中断对象并在以后适当的时间启动队列。

## <a name="child-device-enumeration-pdos-kmdf-only"></a>子设备枚举 (PDOs，KMDF 仅) 


控制总线的驱动程序通常会创建多个设备对象：其角色的 FDO 作为总线本身的函数驱动程序和连接到总线的每个子设备的 PDO。 KMDF 支持子设备的静态和动态枚举。 它还包括其他特定于 PDO 的功能。

即插即用管理器枚举总线时，框架会调用驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 函数。 *EvtDriverDeviceAdd* 为总线创建 FDO，并枚举子设备并为每个设备创建一个 PDO。 驱动程序可以 [静态](static-enumeration.md) 或 [动态地](dynamic-enumeration.md)枚举子设备。

某些回调函数仅适用于代表 PDOs 的设备对象。 当驱动程序初始化设备对象时，它将注册相应的回调。 PDOs 响应有关设备资源和资源要求的查询、锁定或弹出设备的请求，以及启用和禁用设备唤醒信号的请求。

在 WDM 驱动程序中，这些请求作为 [**irp \_ mj \_ PNP**](../kernel/irp-mj-pnp.md) 或 [**irp \_ MJ \_ 电源**](../kernel/irp-mj-power.md) 请求中的次要 IRP 代码到达。 KMDF 驱动程序通过在设备对象初始化过程中通过调用 [**WdfPdoInitSetEventCallbacks**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitseteventcallbacks)来实现回调并注册回调来处理它们。 下表列出了特定于 PDO 的回调：

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query" data-raw-source="[&lt;em&gt;EvtDeviceResourcesQuery&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query)"><em>EvtDeviceResourcesQuery</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resources" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_RESOURCES&lt;/strong&gt;](../kernel/irp-mn-query-resources.md)"><strong>IRP_MN_QUERY_RESOURCES</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query" data-raw-source="[&lt;em&gt;EvtDeviceResourceRequirementsQuery&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query)"><em>EvtDeviceResourceRequirementsQuery</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_RESOURCE_REQUIREMENTS&lt;/strong&gt;](../kernel/irp-mn-query-resource-requirements.md)"><strong>IRP_MN_QUERY_RESOURCE_REQUIREMENTS</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_eject" data-raw-source="[&lt;em&gt;EvtDeviceEject&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_eject)"><em>EvtDeviceEject</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-eject" data-raw-source="[&lt;strong&gt;IRP_MN_EJECT&lt;/strong&gt;](../kernel/irp-mn-eject.md)"><strong>IRP_MN_EJECT</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock" data-raw-source="[&lt;em&gt;EvtDeviceSetLock&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock)"><em>EvtDeviceSetLock</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-lock" data-raw-source="[&lt;strong&gt;IRP_MN_SET_LOCK&lt;/strong&gt;](../kernel/irp-mn-set-lock.md)"><strong>IRP_MN_SET_LOCK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus" data-raw-source="[&lt;em&gt;EvtDeviceEnableWakeAtBus&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus)"><em>EvtDeviceEnableWakeAtBus</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake" data-raw-source="[&lt;strong&gt;IRP_MN_WAIT_WAKE&lt;/strong&gt;](../kernel/irp-mn-wait-wake.md)"><strong>IRP_MN_WAIT_WAKE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus" data-raw-source="[&lt;em&gt;EvtDeviceDisableWakeAtBus&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)"><em>EvtDeviceDisableWakeAtBus</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake" data-raw-source="[&lt;strong&gt;IRP_MN_WAIT_WAKE&lt;/strong&gt;](../kernel/irp-mn-wait-wake.md)"><strong>IRP_MN_WAIT_WAKE</strong></a></p></td>
</tr>
</tbody>
</table>

 

使用其他 **WdfPdoInitXxx** 方法，驱动程序可以指定设备特定的数据，例如设备 id。

 

