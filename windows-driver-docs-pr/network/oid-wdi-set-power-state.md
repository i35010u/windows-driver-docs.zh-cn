---
title: OID_WDI_SET_POWER_STATE
description: OID_WDI_SET_POWER_STATE 设置设备的电源状态。
ms.assetid: f1453ace-5e36-464e-96f0-e578890cdf3f
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_POWER_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fcc41c92d1d38ca43ac1aa6ca9863ca2326e2085
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359204"
---
# <a name="oidwdisetpowerstate"></a>OID\_WDI\_SET\_POWER\_STATE


OID\_WDI\_设置\_POWER\_状态设置设备的电源状态。

| 范围   | 设置与任务序列化 | 正常执行时间 （秒） |
|---------|--------------------------|---------------------------------|
| 适配器 | 是                      | 10                              |

 

NIC 出现在 D0 中 （提供完全支持的设备） 在系统启动时或当 NIC 插入到系统。 条件适合 （AOAC 在平台上，这是 NIC Active 参考为 0 的 NIC 上时），操作系统准备并将 NIC 放入 D0。 如果用户不存在，主机将进入低功耗状态，以节约电源。 主机可能会将 NIC 设置进入低功耗状态，NIC 可以在其中保存自主为主机的连接。 NIC 唤醒外部主机表达感兴趣的事件的主机。

OID\_WDI\_设置\_POWER\_状态到 D0、 D1、 D2 和 D3 设置设备。 D 状态为设备类和特定于平台。 Wi-fi NIC 通常仅支持部分中的状态。 例如，对于 SD 总线上的 Wi-fi 设备，支持的集组成 D0、 D2 和 D3。 D2 和 D3 的含义也是特定于设备。 SDIO 总线上的 Wi-fi nic，它定义要能够从 D2，唤醒，但在 D3，暂停 NIC。

PCIe 总线 NIC 支持 D0 和 D3，其中 D3 可以 D3Hot 或 D3Cold。 在主机软件堆栈，没有仅 D3。 D3hot 或 D3Cold 取决于主机的方案和基础平台支持。 例如，在连接的备用方案，主机将卸载到 NIC 唤醒事件，并将 NIC 设置中 D3，即 D3hot 和平台的支持保持提供支持，以便 NIC 可以监视主机的外部事件的 NIC。 在休眠方案中，主机设置 NIC 中 D3 和平台使 NIC 不使用任何电源关闭 NIC 的幂。

对于支持休眠的 AOAC 系统，以下是重要的系统电源状态的摘要。 在 AOAC 系统中，系统睡眠状态是已连接的备用状态。 这是其中将 Nic 设置为低能耗 （D2 SDBus Nic，D3 PCIe nic） 的状态，能够充分利用唤醒。 如果该驱动程序被挂起到硬盘驱动器，负责驱动程序的恢复，该驱动程序不会通过再次重新初始化的固件状态 （例如，不被称为 DriverEntry）。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>睡眠</th>
<th>休眠</th>
<th>混合关闭</th>
<th>完全关闭</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>通过请求</td>
<td><p>电源按钮 （默认值）</p></td>
<td><p>关闭 /h</p></td>
<td><p>关闭 /s /hybrid</p></td>
<td><p>关闭 /s</p></td>
</tr>
<tr class="even">
<td>UI</td>
<td><p><strong>启动</strong> &gt; <strong>Power</strong> &gt; <strong>进入睡眠状态</strong></p></td>
<td><p>--</p></td>
<td><p><strong>启动</strong> &gt; <strong>Power</strong> &gt; <strong>关闭</strong></p></td>
<td><p>--</p></td>
</tr>
<tr class="odd">
<td>系统状态</td>
<td><p>连接待机</p></td>
<td><p>休眠</p></td>
<td><p>混合关闭</p></td>
<td><p>关机</p></td>
</tr>
<tr class="even">
<td>驱动程序状态</td>
<td><p>保持活动状态-臂唤醒</p></td>
<td><p>挂起到硬盘驱动器</p></td>
<td><p>挂起到硬盘驱动器</p></td>
<td><p>关机</p></td>
</tr>
</tbody>
</table>

 

对于 AOAC 系统休眠状态，不需要或支持，下面是驱动程序的电源状态的摘要。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>睡眠</th>
<th>完全关闭</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>通过请求</td>
<td><p>电源按钮 （默认值）</p></td>
<td><p>关闭 /s</p></td>
</tr>
<tr class="even">
<td>UI</td>
<td><p><strong>启动</strong> &gt; <strong>Power</strong> &gt; <strong>进入睡眠状态</strong></p></td>
<td><p><strong>启动</strong> &gt; <strong>Power</strong> &gt; <strong>关闭</strong></p></td>
</tr>
<tr class="odd">
<td>系统状态</td>
<td><p>连接待机</p></td>
<td><p>关机</p></td>
</tr>
<tr class="even">
<td>驱动程序状态</td>
<td><p>保持活动状态-臂唤醒</p></td>
<td><p>关机</p></td>
</tr>
</tbody>
</table>

 

设置的 power 命令都不能将失败。 固件永远不会将失败，此类命令。 Microsoft 组件可确保不存在任何未完成的任务或命令时将发送任何集电源命令。 未完成设置电源命令时，Microsoft 组件还可确保没有其他的命令或任务发送到 IHV 组件。

| 电源状态                                            | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|--------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| D0 （完全支持）                                     | NIC 已完全通电并且准备好接收命令。 主机永远不会请求低功耗状态之间的更改。 例如，如果宿主希望从 D2 的 NIC 电源状态设置为 D3，它首先设置电源状态到 D0，再到 D3。                                                                                                                                                                                                                                                            |
| D2 和了解唤醒 (SDBus Nic)                     | 在 D2，主机永远不会将请求发送到的固件设置 D0 命令除外。 请参阅本主题的相关流图表后面的部分。                                                                                                                                                                                                                                                                                                                                                                 |
| D3： 关机 (SDBus Nic)，了解唤醒 (PCIe Nic) | 对于 SDBus 的 Nic，此状态下处于关闭状态。 对于 PCIe 总线 Nic，操作系统可能会被唤醒 (D3Hot) 的 arm Nic，或可能会关闭电源 (D3Cold)。 请注意，从驱动程序堆栈的角度来看，没有仅 D3 状态。 涉及多个组件以启用 D3Hot 状态，包括 ACPI 表和 NDIS 系统电源来自具体取决于最终用户操作或而造成，例如休眠状态、 连接待机和混合操作系统的 Irp 的处理关闭。 |
| Dx 为非默认端口的                               | Dx 是 D2 或 D3。 当 NIC 置于的 Dx 所有非默认端口将重置时，这意味着在 Dx 断开连接，所有非默认端口。                                                                                                                                                                                                                                                                                                                                                              |

 

## <a name="set-property-parameters"></a>设置属性参数


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>TLV</th>
<th>允许多个 TLV 实例</th>
<th>可选</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-power-state" data-raw-source="[&lt;strong&gt;WDI_TLV_POWER_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-power-state)"><strong>WDI_TLV_POWER_STATE</strong></a></p></td>
<td></td>
<td></td>
<td><p>电源状态。 这适用于主要的端口。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-enable-wake-events" data-raw-source="[&lt;strong&gt;WDI_TLV_ENABLE_WAKE_EVENTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-enable-wake-events)"><strong>WDI_TLV_ENABLE_WAKE_EVENTS</strong></a></p></td>
<td></td>
<td>X</td>
<td><p>此字段可能只发生在 NIC 正在将进入低能耗和知识来唤醒任何指定的事件 （如 SD io D2)。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-set-power-dx-reason" data-raw-source="[&lt;strong&gt;WDI_TLV_SET_POWER_DX_REASON&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-set-power-dx-reason)"><strong>WDI_TLV_SET_POWER_DX_REASON</strong></a></p></td>
<td></td>
<td>X</td>
<td><p>设置 power 原因。</p></td>
</tr>
</tbody>
</table>

 

## <a name="set-property-results"></a>设置属性结果


| TLV                                                                                 | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                                                                                                                                                                                               |
|-------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_适配器\_恢复\_必需**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-adapter-resume-required) |                                | X        | 如果值为 true，它向 OS 固件需要恢复其上下文的帮助。 这应该只出现时，驱动程序挂起到存储。 由于操作系统发出的一系列的 Wi-fi 命令，将固件上下文和 IHV 组件上下文最新的因此，IHV 组件必须重置软件状态。 |

 

## <a name="enable-wake-events"></a>启用唤醒事件


NIC 指定一组它可以检测唤醒堆栈的事件。 操作系统检测向下部分或完整的低电源命令与该 nic 事件集。 更早于 Dx 命令设置一些唤醒事件参数。 其他人 Dx 命令前设置为固件中。 使用 Dx 命令只会启用所有事件。

在此界面中，设置为启用的事件已经过检测向下可选[ **WDI\_TLV\_启用\_唤醒\_事件**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-enable-wake-events) TLV 作为的一部分OID\_WDI\_设置\_设备电源状态 Dx 的电源命令。 绑定的 TLV 处于不存在如果操作系统不希望 arm 要唤醒的 NIC。

当固件收到具有的 Dx 命令[ **WDI\_TLV\_启用\_唤醒\_事件**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-enable-wake-events)，它可能会检测到在完成 Dx 之前发生唤醒事件命令。 它应缓冲区事件、 完成处理该命令，然后断言唤醒中断。

通过 Wi-fi NIC 的每个唤醒后应执行为什么 NIC 唤醒堆栈的唤醒原因。 NIC 唤醒堆栈通过断言唤醒中断行，这通常由总线或 ACPI 方法提供服务。 这些方法唤醒的 CPU 和所需的组件来处理发生唤醒事件，并完成 Wi-fi 等待唤醒 IRP 堆栈。 随后，操作系统会向驱动程序和固件发出 D0 请求。 此请求是幂 OID 到将 D0 命令发送到固件的驱动程序。 固件保留唤醒原因的指示，直到它接收并完成 D0 命令。

**请注意**  如果 NIC 会收到 D0 命令由于某种原因 （例如，NIC 无法唤醒主机），NIC 应指示唤醒原因。

 

## <a name="no-enabled-wake-events"></a>没有已启用的唤醒的事件


如果没有任何[ **WDI\_TLV\_启用\_唤醒\_事件**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-enable-wake-events)存在，操作系统不需要运行在低功耗的 Nic。 Nic 可能会完全关闭提供支持。 如果挂起到硬盘驱动器，Nic 驱动程序应继续在恢复固件上下文。

## <a name="power-state-interaction-and-transition-examples"></a>电源状态交互和转换示例


以下关系图显示了交互和 D0 和 Dx （D2 或 D3） 之间的转换序列的 nic。 在此上下文中，"微型端口"表示主机或 WDI 兼容的驱动程序。

### <a name="d0-to-dx-armed-to-wake"></a>D0 到 Dx （知识来唤醒）

![wdi d0 dx 有转换](images/wdi-d0-to-dx-armed-to-wake.png)

-   停止\[DnIO |UpIO\]:DnIO 是到较低层的消息 （控件和数据）。 UpIO 是到上层的消息。

    -   拒绝新请求通过层 （快速失败）。
    -   停止 （除非此 Dx 命令） 此层中初始化 IO。
    -   允许注入 TXs 需要进入 Dx 较低层。
    -   刷新队列。
-   AwaitInflight:等待 IO 调用返回，DMA 包括正在进行中。 刷新队列。

-   Dx 是任何非 D0 状态。 有关 SDBus Wi-fi，这是 D2。 对于 PCIe 总线，这是 D3Hot。 固件应不会断电。

### <a name="dx-armed-to-wake-to-d0-transition"></a>Dx （知识来唤醒） D0 转换

![dx 武装 d0 转换到](images/wdi-dx-to-d0-armed-to-wake.png)

-   如果 NIC 有唤醒，它不能为 D3Cold。 固件必须继续在 Dx 中运行。

### <a name="d0-to-d3-not-armed-to-wake-transition"></a>D0 D3 （未配置为能够唤醒） 转换

![d0 d3 不了解转换](images/wdi-d0-to-d3-not-armed.png)

-   停止\[DnIO |UpIO\]:DnIO 是到较低层的消息 （控件和数据）。 UpIO 是到上层的消息。

    -   拒绝新请求通过层 （快速失败）。
    -   停止 （除非此 Dx 命令） 此层中初始化 IO。
    -   允许注入 TXs 需要进入 Dx 较低层。
    -   刷新队列。
-   AwaitInflight:等待 IO 调用返回，DMA 包括正在进行中。 刷新队列。

-   而无需 PmParameters D3。 NIC (D3Cold)，也可能未关闭 （例如，与 D0 设备共享的电源线）。

### <a name="dx-not-armed-to-wake-to-d0-transition"></a>（未配置为能够唤醒） Dx D0 转换

![dx 不具备 d0 转换](images/wdi-dx-to-d0-not-armed.png)

-   D2 notArmToWake:保留的电源，没有所要求的重新初始化。
-   D3 notArmtoWake:可能是热或冷。 冷需要还原该上下文。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




