---
title: NDIS 如何设置网络适配器的电源策略
description: NDIS 如何设置网络适配器的电源策略
keywords:
- 网络接口卡 WDK 网络，电源策略
- Nic WDK 网络，电源策略
- 电源策略 WDK 网络
- DEVICE_CAPABILITIES
- OID_PNP_CAPABILITIES
- 设备电源策略所有者 WDK 网络
- 电源管理 WDK NDIS 微型端口，电源策略
- 用户输入 WDK 电源管理
- 电源管理 WDK NDIS 微型端口，用户输入
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6795808c6f646b470da02c5d3cb6fa567d76e547
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814201"
---
# <a name="how-ndis-sets-the-power-policy-for-a-network-adapter"></a>NDIS 如何设置网络适配器的电源策略





NDIS 充当每个网络设备的设备电源策略所有者。 因此，NDIS 设置并管理每个网络设备的电源策略。 有关管理设备电源策略的详细信息，请参阅 [管理设备电源策略](../kernel/managing-device-power-policy.md)。

NDIS 使用以下信息来设置 NIC 的电源策略：

-   总线驱动程序为响应 IRP 发出的 [**IRP \_ MN \_ 查询 \_ 功能**](../kernel/irp-mn-query-capabilities.md)请求而返回的 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构。

-   小型端口驱动程序对 NDIS 发出的 [OID \_ PNP \_ 功能](./oid-pnp-capabilities.md) 请求的响应。

-   用户界面中的用户输入 (UI) 。

### <a name="using-the-device_capabilities-structure"></a><a href="" id="using-the-device-capabilities-structure"></a>使用设备 \_ 功能结构

枚举 NIC 时，NDIS 还会通过发出 [**IRP \_ MN \_ 查询 \_ 功能**](../kernel/irp-mn-query-capabilities.md) 请求，来查询 nic 的功能。 为响应此请求，总线驱动程序将返回 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities) 结构。 设置 NIC 的电源策略时，NDIS 会复制此结构，并使用此结构中的以下信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/deviced1-and-deviced2" data-raw-source="[DeviceD1 and DeviceD2](../kernel/deviced1-and-deviced2.md)">DeviceD1 和 DeviceD2</a></p></td>
<td align="left"><p>如果设备支持 D1 电源状态，则为 TRUE。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/deviced1-and-deviced2" data-raw-source="[DeviceD1 and DeviceD2](../kernel/deviced1-and-deviced2.md)">DeviceD1 和 DeviceD2</a></p></td>
<td align="left"><p>如果设备支持 D2 电源状态，则为 TRUE。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](../kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)">WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3</a></p></td>
<td align="left"><p>如果设备在处于 D0 电源状态时可以响应外部唤醒信号，则为 TRUE。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](../kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)">WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3</a></p></td>
<td align="left"><p>如果设备在处于 D1 电源状态时可以响应外部唤醒信号，则为 TRUE。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](../kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)">WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3</a></p></td>
<td align="left"><p>如果设备可以在 D2 电源状态下响应外部唤醒信号，则为 TRUE。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](../kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)">WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3</a></p></td>
<td align="left"><p>如果设备在 D3 电源状态下可以响应外部唤醒信号，则为 TRUE。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/devicestate" data-raw-source="[DeviceState](../kernel/devicestate.md)">DeviceState</a><strong>[PowerSystemMaximum]</strong></p></td>
<td align="left"><p>指定此设备可以为每个系统电源状态维持的最高设备状态，从 <strong>PowerSystemUnspecified</strong> 到 <strong>PowerSystemShutdown</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/systemwake" data-raw-source="[SystemWake](../kernel/systemwake.md)">SystemWake</a></p></td>
<td align="left"><p>指定由设备可以向其发出唤醒事件的最小电源状态 (S0 到 S4) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/devicewake" data-raw-source="[DeviceWake](../kernel/devicewake.md)">DeviceWake</a></p></td>
<td align="left"><p>指定 (D0 到 D3) 的最小设备电源状态，设备可从该状态向唤醒事件发出信号。</p></td>
</tr>
</tbody>
</table>

 

NDIS 使用设备 \_ 功能信息来确定：

-   系统和 NIC 都支持电源管理，如果是，则可以在每个系统电源状态中输入 NIC 的设备电源状态。

-   系统和 NIC 都支持 LAN 唤醒，如果是，则 NIC 可从哪个设备电源状态唤醒系统。

**WakeFromD0** 到 **WakeFromD3** 表示 NIC 可从中唤醒系统的设备电源状态。

**DeviceState** 数组指示了每个系统电源状态的最高驱动设备电源状态，在该状态下，NIC 可以同时仍支持系统电源状态。 例如，请考虑下面的数组值。

```cpp
DeviceState[PowerSystemWorking] PowerDeviceD0
DeviceState[PowerSystemSleeping1] PowerDeviceD1
DeviceState[PowerSystemSleeping2] PowerDeviceD2
DeviceState[PowerSystemSleeping3] PowerDeviceD2
DeviceState[PowerSystemHibernate] PowerDeviceD3
DeviceState[PowerSystemShutdown] PowerDeviceD3
```

如前面的示例值数组所示，当系统处于系统电源状态 S1 时，NIC 可以在设备电源状态 D1、D2 或 D3 中。 当系统处于系统电源状态 S2 或 S3 时，NIC 可以位于设备电源状态 D2 或 D3 中。

为了确定系统和 NIC 是否支持 LAN 唤醒，NDIS 同时检查 **SystemWake** 和 **DeviceWake** 成员。 如果将 **SystemWake** 和 **DeviceWake** 都设置为 **POWERSYSTEMUNSPECIFIED**，NDIS 会将 NIC 视为支持电源管理。 在这种情况下，或者如果微型端口驱动程序在初始化过程中将 NDIS 特性设置为 " \_ \_ 挂起时不暂停" \_ \_ \_ 标志，则 NDIS 随后会向微型端口驱动程序发出 [OID \_ PNP \_ 功能](./oid-pnp-capabilities.md) 请求，以获取有关 NIC 的唤醒功能的详细信息。

### <a name="using-oid_pnp_capabilities"></a><a href="" id="using-oid-pnp-capabilities"></a>使用 OID \_ PNP \_ 功能

当微型端口驱动程序成功从其 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数返回后， \_ \_ 如果满足以下任一条件，NDIS 就会向驱动程序发送 OID PNP 功能请求：

-   总线驱动程序返回的 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构的 **SystemWake** 和 **DeviceWake** 成员 *不* 会设置为 **PowerSystemUnspecified**。

-   小型小型驱动程序在 \_ \_ \_ \_ \_ 初始化过程中调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 时，不会对 "挂起" 标志设置 NDIS 特性。

请注意， \_ \_ 不管用户是否在用户界面中启用了 LAN 唤醒，NDIS 都发出 OID PNP 功能请求。

如果微型端口驱动程序返回 NDIS \_ 状态 " \_ 成功" 以响应 [OID \_ PNP \_ 功能](./oid-pnp-capabilities.md)的查询，NDIS 会将微型端口驱动程序视为支持电源管理。 如果微型端口驱动程序返回 \_ \_ 不受支持的 NDIS 状态 \_ ，ndis 会将微型端口驱动程序视为不支持电源管理的旧微型端口驱动程序。 有关此类驱动程序的电源管理的详细信息，请参阅 [旧微型端口驱动程序的电源管理](power-management-for-old-miniport-drivers.md)。

成功执行 OID PNP 功能请求的微型端口驱动程序会 \_ \_ 将以下信息返回给 NDIS，以响应请求：

-   NIC 在收到幻数据包时可以唤醒系统的最小设备电源状态。

-   设备在收到包含协议驱动程序指定模式的网络帧时，可从中唤醒系统的最小设备电源状态。

当 NDIS 获取此信息后，它会确定每个系统电源状态的设备电源状态，如果用户在 UI 中启用了 LAN 唤醒，则可以将其设置为 NIC。 如果没有可供 NIC 从中生成唤醒信号的低功率设备状态 (则为，如果在设备功能结构的 **DeviceState** 阵列中指定的所有低功耗设备电源状态 \_ 低于 nic 可从中唤醒系统) 的最小设备电源状态，NDIS 会使设备在 "**电源管理**" 选项卡中无法使用 nic **来使计算机脱离待机** 状态。 然后，用户无法启用 LAN 唤醒。

**注意**  仅当 NIC 和系统都支持电源管理时，LAN 唤醒才能实现。 如果系统不支持电源管理，NDIS 将不会查询 NIC 的电源管理功能。

 

### <a name="using-user-input"></a>使用用户输入

对于支持电源管理的 NIC，Microsoft Windows 2000 和更高版本在 NIC 的 "**属性**" 对话框的 "**电源管理**" 选项卡中提供以下选项：

**允许计算机关闭此设备以节省电源**

**允许设备使计算机脱离待机状态**

默认情况下，选择第一个选项以启用 NIC 的电源管理。 如果用户清除选项，NDIS 会将 NIC 视为与电源管理有关的旧 NIC。 有关详细信息，请参阅 [旧微型端口驱动程序的电源管理](power-management-for-old-miniport-drivers.md)。

默认情况下，第二个选项是清除的。 如果 NDIS 确定不允许 NIC 从其生成唤醒信号的低功率状态，NDIS 将使第二个选项不可用。 例如，如果设备功能结构的 **DeviceState** 阵列成员 \_ 指示 Nic 必须位于 D3 中以实现所有低功耗系统状态，并且如果 **DeviceWake** 指示 nic 可从其唤醒系统的最低功率设备状态为 D2，则 NDIS 深浅使第二个复选框不可用。

除了上述两个选项以外，Windows XP 和 Windows Vista 还在 NIC 的 " **电源管理** " 选项卡中提供了第三个选项：

**仅允许管理工作站使计算机脱离待机状态**

此选项仅在以下情况下可用，可从属于前面所述的第二个选项：

-   用户选择了第二个选项来启用 LAN 唤醒。

-   小型端口驱动程序在响应 [OID \_ PNP \_ 功能](./oid-pnp-capabilities.md)的情况下，表明 NIC 可以在收到幻数据包时唤醒系统。

默认情况下，" **仅允许管理工作站使计算机退出待机状态** " 选项处于清除状态。 用户可以选择此选项以指定仅接收幻数据包将导致 NIC 生成到系统的唤醒信号。

只要用户为 NIC 选择或清除电源管理选项，系统就会通知 NDIS 发生了更改。 NDIS 将新设置写入注册表，以使更改的设置在重新启动后仍然存在。

