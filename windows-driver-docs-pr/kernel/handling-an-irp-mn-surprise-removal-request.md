---
title: 处理 IRP_MN_SURPRISE_REMOVAL 请求
description: 处理 IRP_MN_SURPRISE_REMOVAL 请求
ms.assetid: 39a90617-40ad-4c10-95d3-2b618d66d70e
keywords:
- 意外删除 WDK PnP
- IRP_MN_SURPRISE_REMOVAL
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a93da8583ab59b3cefb3cdf3f5f58b82c9b4d8d
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106582"
---
# <a name="handling-an-irp_mn_surprise_removal-request"></a>处理 IRP \_ MN \_ 意外 \_ 删除请求





Windows 2000 和更高版本的 PnP 管理器发送此 IRP，通知驱动程序设备不再可用于 i/o 操作，并且可能已从计算机上意外删除 ( "意外删除" ) 。

PnP 管理器发送 [**IRP \_ MN \_ 意外 \_ 删除**](./irp-mn-surprise-removal.md) 请求，原因如下：

-   如果总线具有热插拔通知，它会通知设备的父总线驱动程序设备已消失。 总线驱动程序调用 [**IoInvalidateDeviceRelations**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)。 作为响应，PnP 管理器将查询其子管理器的总线驱动程序， ([**IRP \_ MN \_ QUERY \_ 设备 \_ 关系**](./irp-mn-query-device-relations.md) for **BusRelations**) 。 PnP 管理器确定设备不在新子项列表中，并为设备启动其意外删除操作。

-   由于另一个原因，会枚举总线，而意外删除的设备不会包含在子列表中。 PnP 管理器启动其意外删除操作。

-   设备的函数驱动程序确定设备不再存在 (因为例如，它的请求) 中重复超时。 总线可能可枚举，但它没有热插拔通知。 在这种情况下，函数驱动程序调用 [**IoInvalidateDeviceState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)。 在响应中，PnP 管理器会将 [**IRP \_ MN \_ 查询 \_ PnP \_ 设备 \_ 状态**](./irp-mn-query-pnp-device-state.md) 请求发送到设备堆栈。 函数驱动程序 \_ \_ 在 [**pnp \_ 设备 \_ 状态**](#about-pnp_device_state) 位掩码中设置 pnp 设备失败标志，指示该设备已失败。

-   驱动程序堆栈已成功完成 [**IRP \_ MN \_ 停止 \_ 设备**](./irp-mn-stop-device.md) 请求，但随后无法 [** \_ \_ 启动 \_ 设备**](./irp-mn-start-device.md) 请求。 在这种情况下，设备可能仍处于连接状态。

所有 PnP 驱动程序都必须处理此 IRP，并且必须将 **irp &gt; IoStatus** 设置为状态 " \_ 成功"。 在调用驱动程序的[*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程之后，必须准备 PnP 设备的驱动程序，以便随时处理**IRP \_ MN \_ 意外 \_ 删除**。 正确处理 IRP 后，驱动程序和 PnP 管理器可以：

1.  禁用设备，以防设备仍处于连接状态。

    如果驱动程序堆栈已成功完成 [**IRP \_ MN \_ 停止 \_ 设备**](./irp-mn-stop-device.md) 请求，但出于某种原因，由于某种原因，后续 [**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md) 请求失败，则必须禁用该设备。

2.  释放分配给设备的硬件资源，并将其提供给其他设备。

    一旦某个设备不再可用，其硬件资源就会被释放。 然后，PnP 管理器可以将资源重新分配到另一台设备，包括同一设备，用户可能会将该设备热插回计算机。

3.  最大程度地降低数据丢失和系统中断的风险。

    支持热插拔的设备及其驱动程序应该设计为处理意外删除。 用户希望能够随时删除支持热插拔的设备。

PnP 管理器在系统线程的上下文中以 IRQL = 被动级别发送 **IRP \_ MN \_ 意外 \_ 删除** \_ 。

PnP 管理器会在通知用户模式应用程序和其他内核模式组件之前，将此 IRP 发送到驱动程序。 IRP 完成后，PnP 管理器会将 GUID **EventCategoryTargetDeviceChange** \_ 目标设备删除完成的 EventCategoryTargetDeviceChange 通知发送 \_ \_ \_ 到在设备上注册此类通知的内核模式组件。

**IRP \_ MN \_ 意外 \_ 删除**irp 首先由设备堆栈中的顶层驱动程序处理，然后再由下一个较低的驱动程序处理。

为了响应 **IRP \_ MN \_ 意外 \_ 删除**，驱动程序必须按照列出的顺序执行以下操作：

1.  确定设备是否已删除。

    驱动程序必须始终尝试确定设备是否仍处于连接状态。 如果是，则驱动程序必须尝试停止并禁用该设备。

2.  )  (中断、i/o 端口、内存寄存器和 DMA 通道释放设备的硬件资源。

3.  在父总线驱动程序中，如果驱动程序能够执行此操作，请关闭总线槽。 调用 [**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate) 以通知电源管理器。 有关其他信息，请参阅 [电源管理](./introduction-to-power-management.md)。

4.  防止设备上出现任何新的 i/o 操作。

    驱动程序应处理后续 [**的 irp \_ mj \_ 清理**](./irp-mj-cleanup.md)、 [**irp \_ mj \_ CLOSE**](./irp-mj-close.md)、 [**irp \_ mj \_ 功能**](./irp-mj-power.md)和 [**irp \_ mj \_ PNP**](./irp-mj-pnp.md) 请求，但驱动程序必须阻止任何新的 i/o 操作。 驱动程序必须在设备存在时（除了关闭、清理和 PnP Irp 外），驱动程序可能会处理的任何后续 Irp 失败。

    驱动程序可以在设备扩展中设置一个位，以指示设备已被意外删除。 驱动程序的调度例程应检查此位。

5.  设备上的未完成 i/o 请求失败。

6.  继续向下传递驱动程序未处理设备的任何 Irp。

7.  通过 [**IoSetDeviceInterfaceState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)禁用设备接口。

8.  清理任何特定于设备的分配、内存、事件或其他系统资源。

    驱动程序可以推迟此类清理，直到收到后续的 [**IRP \_ MN \_ REMOVE \_ 设备**](./irp-mn-remove-device.md) 请求，但如果旧组件具有打开的句柄无法关闭，则永远不会发送删除 IRP。

9.  将设备对象保持连接到设备堆栈。

    在后续 **IRP \_ MN \_ 删除 \_ 设备** 请求之前，请勿分离并删除设备对象。

10. 完成 IRP。

    在函数或筛选器驱动程序中：

    -   将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功"。

    -   用 [**IoSkipCurrentIrpStackLocation**](./mm-bad-pointer.md) 设置下一个堆栈位置，并将 IRP 传递到下一个带 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的驱动程序。

    -   将状态从 **IoCallDriver** 作为返回状态从 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程传播。

    -   不要完成 IRP。

    在为子 PDO 处理此 IRP (的总线驱动程序) ：

    -   将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功"。

    -   完成 IRP ([**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) ，IO \_ 无 \_ 增量。

    -   从 *DispatchPnP* 例程返回。

此 IRP 成功并且设备的所有打开的句柄关闭后，PnP 管理器会将 [**IRP \_ MN \_ REMOVE \_ 设备**](./irp-mn-remove-device.md) 请求发送到设备堆栈。 为响应删除 IRP，驱动程序从堆栈中分离其设备对象并将其删除。 如果旧组件具有打开到该设备的句柄，而该句柄仍处于打开状态，但仍有 i/o 故障，则 PnP 管理器从不发送删除 IRP。

所有驱动程序都应该处理此 IRP，并请注意，设备已从计算机中物理删除。 但是，如果不处理 IRP，某些驱动程序将不会产生不良结果。 例如，不使用系统硬件资源并驻留在基于协议的总线上的设备（如 USB 或1394）无法占用硬件资源，因为它不使用任何硬件资源。 由于函数和筛选器驱动程序仅通过父总线驱动程序访问设备，因此在删除设备后，不会有驱动程序尝试访问该设备的风险。 由于总线支持删除通知，因此当设备消失并且总线驱动程序在所有后续尝试访问设备时，会通知父总线驱动程序。

在 Windows 98/Me 上，PnP 管理器不会发送此 IRP。 如果用户在未首先使用相应的用户界面的情况下删除设备，则 PnP 管理器仅向设备驱动程序发送 **IRP \_ MN \_ REMOVE \_ 设备** 请求。 所有 WDM 驱动程序都必须处理 **IRP \_ MN \_ 意外 \_ 删除** 和 **irp \_ MN \_ 删除 \_ 设备**。 **IRP \_ MN \_ REMOVE \_ 设备**的代码应检查驱动程序是否收到了以前的意外删除 IRP，并应处理这两种情况。

 ## <a name="using-guid_reenumerate_self_interface_standard"></a>使用 GUID_REENUMERATE_SELF_INTERFACE_STANDARD

使用 GUID_REENUMERATE_SELF_INTERFACE_STANDARD 接口，驱动程序可以请求其设备 reenumerated。

若要使用此接口，请使用 InterfaceType = GUID_REENUMERATE_SELF_INTERFACE_STANDARD 将 IRP_MN_QUERY_INTERFACE IRP 发送到总线驱动程序。 总线驱动程序提供一个指向 REENUMERATE_SELF_INTERFACE_STANDARD 结构的指针，该结构包含指向接口的各个例程的指针。 [ReenumerateSelf 例程](/windows-hardware/drivers/ddi/wdm/nc-wdm-preenumerate_self)请求总线驱动程序 reenumerate 为子设备。


## <a name="about-pnp_device_state"></a>关于 PNP_DEVICE_STATE

PNP \_ 设备 \_ 状态类型是一个位掩码，用于描述设备的 PNP 状态。 驱动程序将返回此类型的值，以响应 **IRP \_ MN \_ 查询 \_ PNP \_ 设备 \_ 状态** 请求。

``` syntax
typedef ULONG PNP_DEVICE_STATE, *PPNP_DEVICE_STATE;
```

PNP 设备状态值中的标志 \_ 位 \_ 定义如下。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>标志位</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PNP_DEVICE_DISABLED</td>
<td><p>设备在物理上存在，但在硬件中处于禁用状态。</p></td>
</tr>
<tr class="even">
<td>PNP_DEVICE_DONT_DISPLAY_IN_UI</td>
<td><p>不要在用户界面中显示设备。 设置为在当前配置中不能使用的设备，如便携式计算机断开连接时无法使用的便携式计算机上的游戏端口。  (还会在<a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities" data-raw-source="[&lt;strong&gt;DEVICE_CAPABILITIES&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)"><strong>DEVICE_CAPABILITIES</strong></a>结构中看到<strong>NoDisplayInUI</strong>标志。 ) </p></td>
</tr>
<tr class="odd">
<td>PNP_DEVICE_FAILED</td>
<td><p>设备存在，但不能正常工作。</p>
<p>如果同时设置了此标志和 PNP_DEVICE_RESOURCE_REQUIREMENTS_CHANGED，则必须先停止设备，然后 PnP 管理器才能分配新的硬件资源 (不支持设备) 的不间断重新平衡。</p></td>
</tr>
<tr class="even">
<td>PNP_DEVICE_NOT_DISABLEABLE</td>
<td><p>计算机启动时需要设备。 不能禁用此类设备。</p>
<p>驱动程序为适当的系统操作所需的设备设置此位。 例如，如果驱动程序收到通知，表明设备处于寻呼路径 (<a href="irp-mn-device-usage-notification.md" data-raw-source="[&lt;strong&gt;IRP_MN_DEVICE_USAGE_NOTIFICATION&lt;/strong&gt;](irp-mn-device-usage-notification.md)"><strong>IRP_MN_DEVICE_USAGE_NOTIFICATION</strong></a> 用于 <strong>DeviceUsageTypePaging</strong>) ，则驱动程序将调用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate" data-raw-source="[&lt;strong&gt;IoInvalidateDeviceState&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)"><strong>IoInvalidateDeviceState</strong></a> 并在生成的 <strong>IRP_MN_QUERY_PNP_DEVICE_STATE</strong> 请求中设置此标志。</p>
<p>如果为设备设置此位，则 PnP 管理器会将此设置传播到设备的父设备、父设备的父设备等。</p>
<p>如果为根枚举设备设置了此项，则无法禁用或卸载设备。</p></td>
</tr>
<tr class="odd">
<td>PNP_DEVICE_REMOVED</td>
<td><p>设备已被物理删除。</p></td>
</tr>
<tr class="even">
<td>PNP_DEVICE_RESOURCE_REQUIREMENTS_CHANGED</td>
<td><p>设备的资源要求已更改。</p>
<p>通常，当总线驱动程序已确定必须扩展其资源要求以枚举新的子设备时，它将设置此标志。</p></td>
</tr>
<tr class="odd">
<td>PNP_DEVICE_DISCONNECTED</td>
<td><p>已加载设备驱动程序，但该驱动程序检测到设备不再连接到计算机。 通常，此标志用于与无线设备通信的函数驱动程序。 例如，当设备移出范围并在设备移回范围并重新连接后，将设置标志。</p>
<p>总线驱动程序通常不会设置此标志。 如果设备不再处于连接状态，则总线驱动程序应停止枚举子设备。 仅当函数驱动程序管理连接时，才使用此标志。</p>
<p>此标志的唯一用途是让客户端知道设备是否已连接。 设置该标志不会影响是否加载该驱动程序。</p></td>
</tr>
</tbody>
</table>

 

PnP 管理器 \_ \_ 通过将 **IRP \_ MN \_ 查询 \_ PnP \_ 设备 \_ 状态** 请求发送到设备堆栈，在启动设备后立即查询设备的 PnP 设备状态。 为响应此 IRP，设备的驱动程序在 PNP 设备状态中设置相应的 \_ 标志 \_ 。

如果在初始查询后任何状态特征发生更改，驱动程序将通过调用 [**IoInvalidateDeviceState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)通知 PnP 管理器。 为响应对 **IoInvalidateDeviceState**的调用，PnP 管理器会再次查询设备的 PnP \_ 设备 \_ 状态。

如果设备被标记为 PNP \_ 设备 \_ 不 \_ DISABLEABLE，则调试器会显示 devnode 的 DNUF \_ NOT \_ DISABLEABLE 用户标志。 调试器还显示一个 **DisableableDepends** 值，该值计算设备无法禁用的原因数。 此值是 X + Y 的总和，其中 X 为1，如果不能禁用设备，Y 是不能禁用的设备子设备的计数。