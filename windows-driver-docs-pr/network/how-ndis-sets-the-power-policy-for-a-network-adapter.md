---
title: NDIS 如何设置网络适配器的电源策略
description: NDIS 如何设置网络适配器的电源策略
ms.assetid: ede0e33d-16f9-45ec-9e9d-b188f6360b2f
keywords:
- 网络接口卡 WDK 网络、 电源策略
- Nic WDK 网络、 电源策略
- 电源策略 WDK 网络
- DEVICE_CAPABILITIES
- OID_PNP_CAPABILITIES
- 设备电源策略所有者 WDK 联网
- 电源管理 WDK NDIS 微型端口，电源策略
- 用户输入的 WDK 电源管理
- 电源管理 WDK NDIS 微型端口，用户输入
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d49fb0ddb4e2d08a07fa15410ab9453238702abe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360811"
---
# <a name="how-ndis-sets-the-power-policy-for-a-network-adapter"></a>NDIS 如何设置网络适配器的电源策略





NDIS 用作每个网络设备的设备电源策略所有者。 在这种情况下，NDIS 设置和管理每个网络设备的电源策略。 有关管理设备的电源策略的详细信息，请参阅[管理设备的电源策略](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-device-power-policy)。

NDIS 使用以下信息来为 NIC 设置电源策略：

-   [**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)总线驱动程序返回响应的结构[ **IRP\_MN\_查询\_功能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities) NDIS 发出的请求。

-   微型端口驱动程序的响应[OID\_PNP\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)NDIS 发出请求。

-   用户输入从用户界面 (UI)。

### <a href="" id="using-the-device-capabilities-structure"></a>使用设备\_功能结构

NDIS 时枚举 NIC 时，通过发出其他请求，除了查询 NIC 的功能[ **IRP\_MN\_查询\_功能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)请求。 在对此请求的响应，总线驱动程序将返回[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)结构。 NDIS 可将此结构，为 NIC 设置电源策略时使用此结构中的以下信息

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3)">WakeFromD0、 WakeFromD1、 WakeFromD2 和 WakeFromD3</a></p></td>
<td align="left"><p>如果设备可以响应外部唤醒信号中 D0 电源状态，则为 TRUE。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3)">WakeFromD0、 WakeFromD1、 WakeFromD2 和 WakeFromD3</a></p></td>
<td align="left"><p>如果设备可以响应外部唤醒信号中的 D1 电源状态，则为 TRUE。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3)">WakeFromD0、 WakeFromD1、 WakeFromD2 和 WakeFromD3</a></p></td>
<td align="left"><p>如果设备可以响应外部唤醒信号中 D2 电源状态，则为 TRUE。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3)">WakeFromD0、 WakeFromD1、 WakeFromD2 和 WakeFromD3</a></p></td>
<td align="left"><p>如果设备可以响应外部唤醒信号中 D3 电源状态，则为 TRUE。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/devicestate" data-raw-source="[DeviceState](https://docs.microsoft.com/windows-hardware/drivers/kernel/devicestate)">DeviceState</a><strong>[PowerSystemMaximum]</strong></p></td>
<td align="left"><p>指定此设备可以维护的每个系统电源状态，从 highest-powered 设备状态<strong>PowerSystemUnspecified</strong>到<strong>PowerSystemShutdown</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/systemwake" data-raw-source="[SystemWake](https://docs.microsoft.com/windows-hardware/drivers/kernel/systemwake)">SystemWake</a></p></td>
<td align="left"><p>指定最低支持系统电源状态 (通过 S4 S0) 从其设备可以发出信号发生唤醒事件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/devicewake" data-raw-source="[DeviceWake](https://docs.microsoft.com/windows-hardware/drivers/kernel/devicewake)">DeviceWake</a></p></td>
<td align="left"><p>指定最低功率设备电源状态 (通过 D3 D0) 从其设备可以发出信号发生唤醒事件。</p></td>
</tr>
</tbody>
</table>

 

NDIS 使用设备\_功能的信息来确定如果：

-   系统和 NIC 支持电源管理，并且如果是这样，哪些设备电源状态 NIC 可以是为每个系统电源状态。

-   系统和 NIC 支持 LAN 唤醒，和如果是这样，从哪些设备中，电源也状态 NIC 可以将系统唤醒。

**WakeFromD0**通过**WakeFromD3**指示 NIC 可以将系统唤醒从其设备的电源状态。

**DeviceState**数组指示，对于每个系统电源状态，highest-powered 设备电源状态 NIC 可以是和仍支持该系统电源状态。 例如，考虑以下数组值。

```cpp
DeviceState[PowerSystemWorking] PowerDeviceD0
DeviceState[PowerSystemSleeping1] PowerDeviceD1
DeviceState[PowerSystemSleeping2] PowerDeviceD2
DeviceState[PowerSystemSleeping3] PowerDeviceD2
DeviceState[PowerSystemHibernate] PowerDeviceD3
DeviceState[PowerSystemShutdown] PowerDeviceD3
```

如前面的示例值，数组所示，当系统在系统电源状态 S1 中时，NIC 可以是设备电源状态下，D1、 D2 或 D3。 当系统处于系统电源状态 S2 或 S3，NIC 可以是设备电源状态下 D2 或 D3。

若要确定系统和 NIC 是否支持 LAN 唤醒，NDIS 检查这两**SystemWake**并**DeviceWake**成员。 如果这两个**SystemWake**并**DeviceWake**设置为**PowerSystemUnspecified**，NDIS 将视为能使用电源管理的 NIC。 在这种情况下，或如果微型端口驱动程序设置 NDIS\_特性\_否\_暂停\_ON\_挂起标志初始化过程中，随后 NDIS 发出微型端口驱动程序[OID\_PNP\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)请求以获取有关 NIC 的唤醒功能的详细信息。

### <a href="" id="using-oid-pnp-capabilities"></a>使用 OID\_PNP\_功能

后微型端口驱动程序已成功将返回从其[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数，NDIS 发送 OID\_PNP\_对驱动程序如果的功能请求的以下条件为真：

-   这两个**SystemWake**并**DeviceWake**的成员[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)返回的结构总线驱动程序都*不*设置为**PowerSystemUnspecified**。

-   微型端口驱动程序设置 NDIS\_特性\_否\_暂停\_ON\_挂起标志时调用它[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)在初始化过程中。

请注意 NDIS 发出 OID\_PNP\_而不考虑用户是否已启用用户界面中对 LAN 唤醒功能请求。

如果微型端口驱动程序返回 NDIS\_状态\_中的查询响应成功[OID\_PNP\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)，NDIS 将视为电源管理功能的微型端口驱动程序。 如果微型端口驱动程序返回 NDIS\_状态\_不\_支持，NDIS 视为微型端口驱动程序不是电源管理功能的旧微型端口驱动程序。 有关此类驱动程序的电源管理的详细信息，请参阅[旧微型端口驱动程序的电源管理](power-management-for-old-miniport-drivers.md)。

成功 OID 的微型端口驱动程序\_PNP\_功能请求到 NDIS 到请求的响应中返回以下信息：

-   NIC 可以将系统在接收幻数据包唤醒从其最低设备电源状态。

-   NIC 可以接收包含协议驱动程序指定的模式的网络帧上将系统唤醒从其最低设备电源状态。

只要 NDIS 获取此信息，它确定，对于每个系统电源状态，它可以设置为 NIC 如果用户在 UI 中启用了 LAN 唤醒设备的电源状态。 如果没有允许的低功率设备状态从其 NIC 可以生成唤醒信号 (即，如果所有低都功耗设备都电源状态中指定**DeviceState**的设备数组\_功能结构是低于最低的设备的电源状态从其 NIC 可以唤醒系统），使 NDIS**允许设备以使计算机脱离待机状态**选项**电源管理**选项卡不可用的 nic。 然后，用户不能启用 LAN 唤醒。

**请注意**  LAN 唤醒是只有当 NIC 和系统不支持管理的电源。 如果在系统不是电源管理功能，NDIS 将不会查询 NIC 的电源管理功能。

 

### <a name="using-user-input"></a>使用用户输入

有关电源管理支持的 NIC、 Microsoft Windows 2000 和更高版本提供中的下列选项**电源管理**选项卡上的 nic**属性**对话框：

**允许计算机关闭此设备以节约电源**

**允许设备以使计算机脱离待机状态**

默认选择第一个选项以启用电源管理 nic 如果用户清除该选项，NDIS 将 NIC 视为电源管理方面的旧 NIC。 有关详细信息，请参阅[旧微型端口驱动程序的电源管理](power-management-for-old-miniport-drivers.md)。

第二个选项是默认情况下清除。 如果 NDIS 确定 NIC 可以从其生成唤醒信号不允许低功耗状态，则 NDIS 使第二个选项不可用。 例如，如果**DeviceState**设备的数组成员\_功能结构指示对于所有低电源系统状态，必须为在 D3 NIC; 如果**DeviceWake**指示从其 NIC 可以唤醒系统的最低功率设备状态，则 D2，NDIS 灰度梯度使第二个复选框不可用。

除了上述两个选项，Windows XP 和 Windows Vista 提供中的第三个选项**电源管理**NIC 的选项卡：

**仅允许管理工作站，从而使计算机脱离待机状态**

此选项，这是属于前面所述的第二个选项，仅当：

-   用户选择了第二个选项，若要启用 LAN 唤醒。

-   响应中的微型端口驱动程序[OID\_PNP\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)，指示 NIC 无法唤醒接收幻数据包上的系统。

**仅允许管理工作站，从而使计算机脱离待机状态**选项是默认情况下清除。 用户可以选择此选项可指定仅接收幻数据包将导致生成到系统唤醒信号的 NIC。

每次用户选择或清除 NIC 的电源管理选项，则系统会通知更改的 NDIS。 NDIS 写入新设置，对注册表以便更改的设置在重启后仍然存在。

 

 





