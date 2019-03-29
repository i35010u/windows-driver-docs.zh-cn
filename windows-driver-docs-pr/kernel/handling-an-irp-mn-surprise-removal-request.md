---
title: 处理 IRP_MN_SURPRISE_REMOVAL 请求
description: 处理 IRP_MN_SURPRISE_REMOVAL 请求
ms.assetid: 39a90617-40ad-4c10-95d3-2b618d66d70e
keywords:
- 意外删除 WDK 即插即用
- IRP_MN_SURPRISE_REMOVAL
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20fb386fe4e7a23e0ff63f00357f3eb8b4d0b1f2
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349792"
---
# <a name="handling-an-irpmnsurpriseremoval-request"></a>处理 IRP\_MN\_惊讶\_删除请求





在 Windows 2000 和更高版本 PnP 管理器将发送此 IRP 通知驱动程序设备不再可用于 I/O 操作，可能已被意外删除的计算机 （"意外删除"）。

PnP 管理器将发送[ **IRP\_MN\_惊讶\_删除**](https://msdn.microsoft.com/library/windows/hardware/ff551760)请求原因如下：

-   如果在总线具有热即插即用通知，它将通知设备的父总线驱动程序，该设备已消失。 总线驱动程序调用[ **IoInvalidateDeviceRelations**](https://msdn.microsoft.com/library/windows/hardware/ff549353)。 在响应中，即插即用管理器将为子查询总线驱动程序 ([**IRP\_MN\_查询\_设备\_关系**](https://msdn.microsoft.com/library/windows/hardware/ff551670)为**BusRelations**)。 PnP 管理器确定设备在新的子级列表中不是启动设备及其在意外删除操作。

-   总线枚举由于其他原因和意外删除设备不包括在子级的列表。 PnP 管理器会启动其意外删除操作。

-   设备功能驱动程序确定设备不再存在 （因为，例如，其请求重复时间设置超时）。 总线可能是可枚举，但它不具有热即插即用通知。 在这种情况下，功能驱动程序调用[ **IoInvalidateDeviceState**](https://msdn.microsoft.com/library/windows/hardware/ff549361)。 在响应中，即插即用管理器将发送[ **IRP\_MN\_查询\_PNP\_设备\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff551698)对设备堆栈请求。 功能驱动程序设置 PNP\_设备\_中的失败标志[ **PNP\_设备\_状态**](#about-pnp_device_state)位掩码，指示该设备已失败。

-   已成功完成驱动程序堆栈[ **IRP\_MN\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551755)请求但随后失败的后续[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求。 在这种情况下，可能仍连接设备。

所有即插即用驱动程序必须处理此 IRP，必须设置**Irp-&gt;IoStatus.Status**于状态\_成功。 即插即用设备的驱动程序必须准备好处理**IRP\_MN\_惊讶\_删除**后，驱动程序的任何时候[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)调用例程。 正确处理 IRP 启用的驱动程序和即插即用管理器:

1.  在仍处于连接状态的情况下禁用该设备。

    如果已成功完成驱动程序堆栈[ **IRP\_MN\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551755)请求但随后出于某种原因，无法后续[**IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求，必须禁用设备。

2.  释放分配给设备的硬件资源，并将它们提供给另一台设备。

    只要设备不再可用，应释放它的硬件资源。 PnP 管理器然后可以重新分配到另一个设备，包括在同一设备，该用户可能热插拔回计算机的资源。

3.  最大程度减少数据丢失和系统中断的风险。

    设备支持热插拔和其驱动程序应设计为处理意外删除。 用户希望能够在任何时间都支持热插拔的设备中删除。

PnP 管理器将发送**IRP\_MN\_惊讶\_删除**在 IRQL = 被动\_级别在系统线程的上下文中。

PnP 管理器通知用户模式应用程序和其他内核模式组件之前将此 IRP 发送到驱动程序。 IRP 完成后，即插即用管理器将发送**EventCategoryTargetDeviceChange**通知 guid\_目标\_设备\_删除\_完成到内核模式为此类通知在设备上注册的组件。

**IRP\_MN\_惊讶\_删除**设备堆栈中顶部驱动程序，然后按每个下一步的较低的驱动程序第一次处理 IRP。

以响应**IRP\_MN\_惊讶\_删除**，驱动程序必须执行以下操作，列出的顺序：

1.  确定是否已删除设备。

    该驱动程序必须始终尝试确定设备是否仍要连接。 如果是，驱动程序必须尝试停用设备并将其禁用。

2.  释放 （中断、 I/O 端口、 内存寄存器和 DMA 通道） 的设备的硬件资源。

3.  在父总线驱动程序，断开电源总线槽驱动程序是否能够执行此操作。 调用[ **PoSetPowerState** ](https://msdn.microsoft.com/library/windows/hardware/ff559765)通知电源管理器。 有关其他信息，请参阅[电源管理](implementing-power-management.md)。

4.  阻止任何新的 I/O 操作在设备上。

    驱动程序应处理后续[ **IRP\_MJ\_清理**](https://msdn.microsoft.com/library/windows/hardware/ff550718)， [ **IRP\_MJ\_关闭**](https://msdn.microsoft.com/library/windows/hardware/ff550720)， [ **IRP\_MJ\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff550784)，并且[ **IRP\_MJ\_PNP**](https://msdn.microsoft.com/library/windows/hardware/ff550772)请求，但该驱动程序必须阻止任何新的 I/O 操作。 驱动程序时不能将已处理驱动程序，如果设备已存在，除了关闭、 清理和 PnP Irp 任何后续 Irp。

    驱动程序可以设置有点设备扩展中，指示设备已被意外删除。 驱动程序的调度例程应检查此位。

5.  在设备上的未完成 I/O 请求失败。

6.  继续将向设备驱动程序不处理任何 Irp 下传递。

7.  禁用设备配合[ **IoSetDeviceInterfaceState**](https://msdn.microsoft.com/library/windows/hardware/ff549700)。

8.  清理任何特定于设备的分配、 内存、 事件或其他系统资源。

    驱动程序无法推迟此类清理，直到收到后续[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)请求，但是如果的旧组件有一个打开的句柄无法关闭，将永远不会发送 IRP 删除。

9.  将设备对象附加到设备堆栈。

    不分离和删除的设备对象到后续**IRP\_MN\_删除\_设备**请求。

10. 完成 IRP。

    在函数或筛选器驱动程序：

    -   设置**Irp-&gt;IoStatus.Status**于状态\_成功。

    -   设置下一步堆栈位置与[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355) ，并将 IRP 传递到下一个较低的驱动程序与[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336).

    -   传播将状态从**IoCallDriver**作为返回的状态[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

    -   无法完成 IRP。

    在总线驱动程序 （这针对子级 PDO 处理此 IRP）：

    -   设置**Irp-&gt;IoStatus.Status**于状态\_成功。

    -   完成 IRP ([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)) 与 IO\_否\_增量。

    -   返回从*DispatchPnP*例程。

此 IRP 成功关闭所有打开的句柄到设备之后，即插即用管理器将发送[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)对设备堆栈请求。 以响应删除 IRP，驱动程序及其设备对象从堆栈中分离和删除它们。 如果旧组件有打开到设备的句柄，并且它留句柄打开尽管 I/O 故障，即插即用管理器永远不会发送删除 IRP。

所有驱动程序应处理此 IRP，并应记下已以物理方式从计算机删除设备。 某些驱动程序，但是，将不会造成负面结果不会处理 IRP。 例如，因为它不占用任何会占用任何系统硬件资源，并且位于基于协议的总线，如 USB 或 1394年上的设备不能占用硬件资源。 不存在的驱动程序尝试访问设备后的函数和筛选器驱动程序只能通过父总线驱动程序访问设备，因此它已删除的风险。 由于在总线支持删除通知，如果该设备将消失，并且总线驱动程序无法访问设备的所有后续尝试通知父总线驱动程序。

在 Windows 98 上 / 我，即插即用管理器不会发送此 IRP。 如果用户删除设备时无需先使用相应的用户界面，即插即用管理器仅发送**IRP\_MN\_删除\_设备**到设备的驱动程序的请求。 所有 WDM 驱动程序必须都处理两者**IRP\_MN\_惊讶\_删除**并**IRP\_MN\_删除\_设备**。 代码**IRP\_MN\_删除\_设备**应检查是否该驱动程序收到先前的意外删除 IRP，应处理这两种情况。

 ## <a name="using-guidreenumerateselfinterfacestandard"></a>使用 GUID_REENUMERATE_SELF_INTERFACE_STANDARD

GUID_REENUMERATE_SELF_INTERFACE_STANDARD 接口，请求重新枚举其设备的驱动程序。

若要使用此接口，请将 IRP_MN_QUERY_INTERFACE IRP 发送到总线驱动程序与 InterfaceType = GUID_REENUMERATE_SELF_INTERFACE_STANDARD。 总线驱动程序提供了指向包含该接口的单个例程的指针的 REENUMERATE_SELF_INTERFACE_STANDARD 结构的指针。 一个[ReenumerateSelf 例程](https://msdn.microsoft.com/library/windows/hardware/ff560837)总线驱动程序 reenumerate 子设备的请求。


## <a name="about-pnpdevicestate"></a>有关 PNP_DEVICE_STATE

PNP\_设备\_状态类型是一个位掩码，说明设备的即插即用状态。 驱动程序将在响应中返回此类型的值**IRP\_MN\_查询\_PNP\_设备\_状态**请求。

``` syntax
typedef ULONG PNP_DEVICE_STATE, *PPNP_DEVICE_STATE;
```

PNP 中的标志位\_设备\_STATE 值定义，如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>标志位</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PNP_DEVICE_DISABLED</td>
<td><p>设备实际存在，但在硬件中禁用。</p></td>
</tr>
<tr class="even">
<td>PNP_DEVICE_DONT_DISPLAY_IN_UI</td>
<td><p>在用户界面中不显示该设备。 设置是以物理方式存在但不是能使用的当前配置，如便携式计算机未插接时不可用的便携式计算机上的游戏端口的设备。 (另请参阅<strong>NoDisplayInUI</strong>中的标志<a href="https://msdn.microsoft.com/library/windows/hardware/ff543095" data-raw-source="[&lt;strong&gt;DEVICE_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543095)"> <strong>DEVICE_CAPABILITIES</strong> </a>结构。)</p></td>
</tr>
<tr class="odd">
<td>PNP_DEVICE_FAILED</td>
<td><p>设备已存在但没有正常工作。</p>
<p>当设置此标志和 PNP_DEVICE_RESOURCE_REQUIREMENTS_CHANGED 时，设备必须先停止即插即用管理器将分配新的硬件资源 （不间断重新平衡不支持的设备）。</p></td>
</tr>
<tr class="even">
<td>PNP_DEVICE_NOT_DISABLEABLE</td>
<td><p>在计算机启动时需要该设备。 此类设备不能禁用。</p>
<p>驱动程序设置此位的设备的是正确的系统操作所必需的。 例如，如果驱动程序将收到通知，设备已分页路径中 (<a href="irp-mn-device-usage-notification.md" data-raw-source="[&lt;strong&gt;IRP_MN_DEVICE_USAGE_NOTIFICATION&lt;/strong&gt;](irp-mn-device-usage-notification.md)"><strong>IRP_MN_DEVICE_USAGE_NOTIFICATION</strong> </a>有关<strong>DeviceUsageTypePaging</strong>)，该驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff549361" data-raw-source="[&lt;strong&gt;IoInvalidateDeviceState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549361)"> <strong>IoInvalidateDeviceState</strong> </a> ，并在生成中设置此标志<strong>IRP_MN_QUERY_PNP_DEVICE_STATE</strong>请求。</p>
<p>如果设备设置此位，即插即用管理器将传播此设置设置为父设备、 其父级的父设备等。</p>
<p>如果根枚举的设备设置此位，则不能禁用或卸载设备。</p></td>
</tr>
<tr class="odd">
<td>PNP_DEVICE_REMOVED</td>
<td><p>已以物理方式删除设备。</p></td>
</tr>
<tr class="even">
<td>PNP_DEVICE_RESOURCE_REQUIREMENTS_CHANGED</td>
<td><p>已更改设备的资源要求。</p>
<p>通常情况下，总线驱动程序设置此标志，当它认为它必须展开其资源要求，以便枚举新的子设备。</p></td>
</tr>
<tr class="odd">
<td>PNP_DEVICE_DISCONNECTED</td>
<td><p>加载设备驱动程序，但此驱动程序已检测到该设备无法再连接到计算机。 通常情况下，此标志用于功能与无线设备进行通信的驱动程序。 例如，如果设备移出范围，并在设备移动到目标范围，并重新连接之后清除设置标志。</p>
<p>总线驱动程序通常不设置此标志。 总线驱动程序应改为停止枚举子设备，如果设备已断开连接。 功能驱动程序管理的连接时，才使用此标志。</p>
<p>此标志的唯一目的是让客户端知道设备是否已连接。 将此标志设置不影响是否加载了驱动程序。</p></td>
</tr>
</tbody>
</table>

 

PnP 管理器将查询设备的 PNP\_设备\_之后启动设备发送的状态**IRP\_MN\_查询\_PNP\_设备\_状态**对设备堆栈请求。 在响应此 IRP，设备的驱动程序设置适当的标记中 PNP\_设备\_状态。

如果状态特征中的任何更改后的初始查询，请将驱动程序通知即插即用管理器通过调用[ **IoInvalidateDeviceState**](https://msdn.microsoft.com/library/windows/hardware/ff549361)。 中的调用的响应**IoInvalidateDeviceState**，即插即用管理器将查询设备的 PNP\_设备\_再次状态。

如果设备被标记为 PNP\_设备\_不\_DISABLEABLE，调试器将显示 DNUF\_不\_devnode DISABLEABLE 用户标志。 调试器还会显示**DisableableDepends**原因为何不能禁用设备的数目进行计数的值。 此值是 X + Y，其中 X 是一个如果设备不能被禁用，Y 是不能禁用的设备的子设备数之和。




