---
title: NDIS 如何设置网络适配器的电源策略
description: NDIS 如何设置网络适配器的电源策略
ms.assetid: ede0e33d-16f9-45ec-9e9d-b188f6360b2f
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
ms.openlocfilehash: 781bcb6698977493af8e47e1474150de652ef2e6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842541"
---
# <a name="how-ndis-sets-the-power-policy-for-a-network-adapter"></a>NDIS 如何设置网络适配器的电源策略





NDIS 充当每个网络设备的设备电源策略所有者。 因此，NDIS 设置并管理每个网络设备的电源策略。 有关管理设备电源策略的详细信息，请参阅[管理设备电源策略](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-device-power-policy)。

NDIS 使用以下信息来设置 NIC 的电源策略：

-   总线驱动程序为响应[**IRP\_MN\_查询\_功能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)请求而返回的[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构。

-   小型端口驱动程序对由 NDIS 发出[\_PNP\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)请求的 OID 的响应。

-   用户界面（UI）中的用户输入。

### <a href="" id="using-the-device-capabilities-structure"></a>使用设备\_功能结构

枚举 NIC 时，除了其他请求，NDIS [ **\_MN\_查询\_功能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)请求之外，NDIS 还会查询 nic 的功能。 为响应此请求，总线驱动程序将返回[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构。 设置 NIC 的电源策略时，NDIS 会复制此结构，并使用此结构中的以下信息。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/deviced1-and-deviced2" data-raw-source="[DeviceD1 and DeviceD2](https://docs.microsoft.com/windows-hardware/drivers/kernel/deviced1-and-deviced2)">DeviceD1 和 DeviceD2</a></p></td>
<td align="left"><p>如果设备支持 D1 电源状态，则为 TRUE。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/deviced1-and-deviced2" data-raw-source="[DeviceD1 and DeviceD2](https://docs.microsoft.com/windows-hardware/drivers/kernel/deviced1-and-deviced2)">DeviceD1 和 DeviceD2</a></p></td>
<td align="left"><p>如果设备支持 D2 电源状态，则为 TRUE。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3)">WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3</a></p></td>
<td align="left"><p>如果设备在处于 D0 电源状态时可以响应外部唤醒信号，则为 TRUE。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3)">WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3</a></p></td>
<td align="left"><p>如果设备在处于 D1 电源状态时可以响应外部唤醒信号，则为 TRUE。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3)">WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3</a></p></td>
<td align="left"><p>如果设备可以在 D2 电源状态下响应外部唤醒信号，则为 TRUE。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3)">WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3</a></p></td>
<td align="left"><p>如果设备在 D3 电源状态下可以响应外部唤醒信号，则为 TRUE。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/devicestate" data-raw-source="[DeviceState](https://docs.microsoft.com/windows-hardware/drivers/kernel/devicestate)">DeviceState</a><strong>[PowerSystemMaximum]</strong></p></td>
<td align="left"><p>指定此设备可以为每个系统电源状态维持的最高设备状态，从<strong>PowerSystemUnspecified</strong>到<strong>PowerSystemShutdown</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/systemwake" data-raw-source="[SystemWake](https://docs.microsoft.com/windows-hardware/drivers/kernel/systemwake)">SystemWake</a></p></td>
<td align="left"><p>指定设备可以从其发出唤醒事件信号的最低功率系统电源状态（S0 到 S4）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/devicewake" data-raw-source="[DeviceWake](https://docs.microsoft.com/windows-hardware/drivers/kernel/devicewake)">DeviceWake</a></p></td>
<td align="left"><p>指定设备可用于向唤醒事件发出信号的最小设备电源状态（D0 到 D3）。</p></td>
</tr>
</tbody>
</table>

 

NDIS 使用设备\_功能信息来确定：

-   系统和 NIC 都支持电源管理，如果是，则可以在每个系统电源状态中输入 NIC 的设备电源状态。

-   系统和 NIC 都支持 LAN 唤醒，如果是，则 NIC 可从哪个设备电源状态唤醒系统。

**WakeFromD0**到**WakeFromD3**表示 NIC 可从中唤醒系统的设备电源状态。

**DeviceState**数组指示了每个系统电源状态的最高驱动设备电源状态，在该状态下，NIC 可以同时仍支持系统电源状态。 例如，请考虑下面的数组值。

```cpp
DeviceState[PowerSystemWorking] PowerDeviceD0
DeviceState[PowerSystemSleeping1] PowerDeviceD1
DeviceState[PowerSystemSleeping2] PowerDeviceD2
DeviceState[PowerSystemSleeping3] PowerDeviceD2
DeviceState[PowerSystemHibernate] PowerDeviceD3
DeviceState[PowerSystemShutdown] PowerDeviceD3
```

如前面的示例值数组所示，当系统处于系统电源状态 S1 时，NIC 可以在设备电源状态 D1、D2 或 D3 中。 当系统处于系统电源状态 S2 或 S3 时，NIC 可以位于设备电源状态 D2 或 D3 中。

为了确定系统和 NIC 是否支持 LAN 唤醒，NDIS 同时检查**SystemWake**和**DeviceWake**成员。 如果将**SystemWake**和**DeviceWake**都设置为**POWERSYSTEMUNSPECIFIED**，NDIS 会将 NIC 视为支持电源管理。 在这种情况下，或者如果微型端口驱动程序将 NDIS\_属性设置\_在初始化期间\_暂停标志上不\_停止\_，NDIS 随后会向微型端口驱动程序颁发[OID\_PNP\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)请求获取有关 NIC 的唤醒功能的详细信息。

### <a href="" id="using-oid-pnp-capabilities"></a>使用 OID\_PNP\_功能

当微型端口驱动程序成功从其[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数返回后，如果满足以下任一条件，NDIS 会向驱动程序发送 OID\_PNP\_功能请求：

-   设备的**SystemWake**和**DeviceWake**成员\_的总线驱动程序返回的[**功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构*不*会设置为**PowerSystemUnspecified**。

-   微型端口驱动程序将 NDIS\_属性设置\_在初始化期间调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)时，不\_停止\_在\_暂停标志上。

请注意，无论用户是否在用户界面中启用了 LAN 唤醒，NDIS 都\_PNP\_功能请求发出 OID。

如果微型端口驱动程序返回 NDIS\_状态\_成功响应[OID\_PNP\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)的查询，NDIS 会将微型端口驱动程序视为支持电源管理。 如果微型端口驱动程序返回 NDIS\_状态\_不\_支持，NDIS 会将微型端口驱动程序视为不支持电源管理的旧微型端口驱动程序。 有关此类驱动程序的电源管理的详细信息，请参阅[旧微型端口驱动程序的电源管理](power-management-for-old-miniport-drivers.md)。

成功\_PNP\_功能请求的微型端口驱动程序会将以下信息返回给 NDIS，以响应请求：

-   NIC 在收到幻数据包时可以唤醒系统的最小设备电源状态。

-   设备在收到包含协议驱动程序指定模式的网络帧时，可从中唤醒系统的最小设备电源状态。

当 NDIS 获取此信息后，它会确定每个系统电源状态的设备电源状态，如果用户在 UI 中启用了 LAN 唤醒，则可以将其设置为 NIC。 如果没有可供 NIC 从中生成唤醒信号的低功率设备状态（即，如果在\_设备的**DeviceState**数组中指定的所有低功耗设备电源状态都低于最低NIC 可从其唤醒系统的设备电源状态，NDIS 使设备在 "**电源管理**" 选项卡中无法使用 nic 时，使**设备进入待机**状态。 然后，用户无法启用 LAN 唤醒。

**请注意**，只有在 NIC 和系统都支持电源管理的情况下，  LAN 唤醒才能实现。 如果系统不支持电源管理，NDIS 将不会查询 NIC 的电源管理功能。

 

### <a name="using-user-input"></a>使用用户输入

对于支持电源管理的 NIC，Microsoft Windows 2000 和更高版本在 NIC 的 "**属性**" 对话框的 "**电源管理**" 选项卡中提供以下选项：

**允许计算机关闭此设备以节省电源**

**允许设备使计算机脱离待机状态**

默认情况下，选择第一个选项以启用 NIC 的电源管理。 如果用户清除选项，NDIS 会将 NIC 视为与电源管理有关的旧 NIC。 有关详细信息，请参阅[旧微型端口驱动程序的电源管理](power-management-for-old-miniport-drivers.md)。

默认情况下，第二个选项是清除的。 如果 NDIS 确定不允许 NIC 从其生成唤醒信号的低功率状态，NDIS 将使第二个选项不可用。 例如，如果设备的**DeviceState**阵列成员\_功能结构指示 nic 必须在 D3 中适用于所有低功耗系统状态，并且**DeviceWake**指示 nic 的最小设备状态可以唤醒系统为 D2，而 NDIS 暗色使第二个复选框不可用。

除了上述两个选项以外，Windows XP 和 Windows Vista 还在 NIC 的 "**电源管理**" 选项卡中提供了第三个选项：

**仅允许管理工作站使计算机脱离待机状态**

此选项仅在以下情况下可用，可从属于前面所述的第二个选项：

-   用户选择了第二个选项来启用 LAN 唤醒。

-   小型端口驱动程序在响应[OID\_PNP\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)时，表明 NIC 可以在收到幻数据包时唤醒系统。

默认情况下，"**仅允许管理工作站使计算机退出待机状态**" 选项处于清除状态。 用户可以选择此选项以指定仅接收幻数据包将导致 NIC 生成到系统的唤醒信号。

只要用户为 NIC 选择或清除电源管理选项，系统就会通知 NDIS 发生了更改。 NDIS 将新设置写入注册表，以使更改的设置在重新启动后仍然存在。

 

 





