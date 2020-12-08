---
title: OID_WDI_SET_POWER_STATE
description: OID_WDI_SET_POWER_STATE 设置设备的电源状态。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_POWER_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 73dc2bfc598e76d63b7adf1b12d78ccb7a660403
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829345"
---
# <a name="oid_wdi_set_power_state"></a>OID \_ WDI \_ 设置 \_ 电源 \_ 状态


OID \_ WDI \_ 设置 \_ 电源 \_ 状态设置设备的电源状态。

| 范围   | 设置序列化任务 | 正常执行时间 (秒)  |
|---------|--------------------------|---------------------------------|
| 适配器 | 是                      | 10                              |

 

当系统启动或 NIC 接通电源时，NIC 将以 D0 (设备处于完全开机) 。 如果条件在 AOAC 平台上是正确的 (，则这是 NIC 活动引用在 NIC) 上为0时，操作系统将准备该 nic 并将其放入 D0。 如果用户不存在，则主机进入低功耗状态以节省电能。 主机可以将 NIC 设置为较低的电源状态，在该状态下，NIC 可以为主机保持独立连接。 NIC 唤醒主机以获取主机表示兴趣的外部事件。

OID \_ WDI \_ 设置 \_ 电源 \_ 状态会将设备设置为 D0、D1、D2 和 D3。 D 状态是设备类和特定于平台的。 Wi-Fi NIC 通常仅支持部分状态。 例如，对于 SD bus 上 Wi-Fi 设备，受支持的集由 D0、D2 和 D3 组成。 D2 和 D3 的含义也是设备特定的。 对于 SDIO 总线上的 Wi-Fi NIC，定义为能够从 D2 唤醒，但在 D3 中，NIC 被停止。

PCIe 总线 NIC 支持 D0 和 D3，其中 D3 可以是 D3Hot 或 D3Cold。 主机软件堆栈上只有 D3。 D3hot 或 D3Cold 依赖于主机方案和基础平台支持。 例如，在连接待机情况下，主机会将唤醒事件卸载到 NIC，并在 D3 中设置 NIC，这与平台支持 D3hot，使 nic 能够监视主机的外部事件。 在休眠情况下，主机在 D3 中设置 NIC，平台关闭 NIC 电源，使 NIC 不使用任何电源。

对于支持休眠的 AOAC 系统，以下是重要系统电源状态的摘要。 在 AOAC 系统中，系统睡眠状态是 "连接待机" 状态。 这是 Nic 设置为低功耗 (D2 的状态，适用于 PCIe Nic 的 D3) 并唤醒。 如果驱动程序已挂起到硬盘驱动器，则驱动程序将负责恢复固件状态，因为驱动程序不会再次初始化， (例如，DriverEntry 不会) 。

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
<th>睡眠状态</th>
<th>而后</th>
<th>混合关闭</th>
<th>完全关闭</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>请求者</td>
<td><p>电源按钮 (默认值) </p></td>
<td><p>关机/h</p></td>
<td><p>关机/s/hybrid</p></td>
<td><p>关机/s</p></td>
</tr>
<tr class="even">
<td>UI</td>
<td><p><strong>开始</strong> &gt;<strong>电源</strong> &gt;<strong>睡眠</strong></p></td>
<td><p>--</p></td>
<td><p><strong>开始</strong> &gt;<strong>电源</strong> &gt;<strong>关闭</strong></p></td>
<td><p>--</p></td>
</tr>
<tr class="odd">
<td>系统状态</td>
<td><p>连接待机</p></td>
<td><p>而后</p></td>
<td><p>混合关闭</p></td>
<td><p>关机</p></td>
</tr>
<tr class="even">
<td>驱动程序状态</td>
<td><p>活动-唤醒</p></td>
<td><p>挂起到硬盘驱动器</p></td>
<td><p>挂起到硬盘驱动器</p></td>
<td><p>关机</p></td>
</tr>
</tbody>
</table>

 

对于不需要或不支持休眠的 AOAC 系统，以下是驱动程序电源状态的摘要。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>睡眠状态</th>
<th>完全关闭</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>请求者</td>
<td><p>电源按钮 (默认值) </p></td>
<td><p>关机/s</p></td>
</tr>
<tr class="even">
<td>UI</td>
<td><p><strong>开始</strong> &gt;<strong>电源</strong> &gt;<strong>睡眠</strong></p></td>
<td><p><strong>开始</strong> &gt;<strong>电源</strong> &gt;<strong>关闭</strong></p></td>
</tr>
<tr class="odd">
<td>系统状态</td>
<td><p>连接待机</p></td>
<td><p>关机</p></td>
</tr>
<tr class="even">
<td>驱动程序状态</td>
<td><p>活动-唤醒</p></td>
<td><p>关机</p></td>
</tr>
</tbody>
</table>

 

设置电源命令不会失败。 该固件绝不会导致此类命令失败。 Microsoft 组件可确保在发送任何设置的 power 命令时，没有未完成的任务或命令。 当 "设置电源" 命令未完成时，Microsoft 组件还保证不会将其他命令或任务发送到 IHV 组件。

| 电源状态                                            | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|--------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| D0 (完全开机)                                      | NIC 已完全供电，可以接收命令。 主机绝不会请求在低功耗状态之间进行更改。 例如，如果主机要设置从 D2 到 D3 的 NIC 电源状态，它首先将电源状态设置为 D0，然后将其设置为 D3。                                                                                                                                                                                                                                                            |
| D2 和用于唤醒 (SDBus Nic)                      | 在 D2 中，主机绝不会向固件发送请求，但设置 D0 命令除外。 请参阅本主题的后面部分，了解相关流程图。                                                                                                                                                                                                                                                                                                                                                                 |
| D3： power off (SDBus Nic) ，为唤醒 (PCIe Nic 提供的功能)  | 对于 SDBus Nic，此状态为 "已关闭"。 对于 PCIe 总线 Nic，操作系统可以通过 arm Nic (D3Hot) 唤醒，也可以关闭 power (D3Cold) 。 请注意，从驱动程序堆栈角度来看，只有 D3 状态。 要启用 D3Hot 状态，需要使用多个组件，包括 ACPI 表和来自操作系统的 NDIS 系统电源 Irp 处理（具体取决于最终用户操作或由），如休眠、连接待机和混合关闭。 |
| 用于非默认端口的 Dx                               | Dx 为 D2 或 D3。 将 NIC 置于 Dx 后，所有非默认端口都将重置，这意味着所有非默认端口都将在 Dx 中断开连接。                                                                                                                                                                                                                                                                                                                                                              |

 

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
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/network/wdi-tlv-power-state" data-raw-source="[&lt;strong&gt;WDI_TLV_POWER_STATE&lt;/strong&gt;](./wdi-tlv-power-state.md)"><strong>WDI_TLV_POWER_STATE</strong></a></p></td>
<td></td>
<td></td>
<td><p>电源状态。 这适用于主端口。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/network/wdi-tlv-enable-wake-events" data-raw-source="[&lt;strong&gt;WDI_TLV_ENABLE_WAKE_EVENTS&lt;/strong&gt;](./wdi-tlv-enable-wake-events.md)"><strong>WDI_TLV_ENABLE_WAKE_EVENTS</strong></a></p></td>
<td></td>
<td>X</td>
<td><p>此字段可能仅在以下情况下才会出现：将 NIC 置于低功耗，并唤醒任何指定的事件 (如在 SD IO) 上的 D2。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/network/wdi-tlv-set-power-dx-reason" data-raw-source="[&lt;strong&gt;WDI_TLV_SET_POWER_DX_REASON&lt;/strong&gt;](./wdi-tlv-set-power-dx-reason.md)"><strong>WDI_TLV_SET_POWER_DX_REASON</strong></a></p></td>
<td></td>
<td>X</td>
<td><p>设置的电源原因。</p></td>
</tr>
</tbody>
</table>

 

## <a name="set-property-results"></a>设置属性结果


| TLV                                                                                 | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                                                                                                                                                                                                               |
|-------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 适配器 \_ \_ 需要恢复**](./wdi-tlv-adapter-resume-required.md) |                                | X        | 如果该值为 true，则向操作系统发出信号，指示固件在恢复其上下文时需要帮助。 仅当驱动程序挂起到存储时才会出现这种情况。 IHV 组件必须重置软件状态，因为操作系统会发出一系列 Wi-Fi 命令，使固件上下文和 IHV 组件上下文保持最新。 |

 

## <a name="enable-wake-events"></a>启用唤醒事件


NIC 指定它可以检测到的用于唤醒堆栈的事件集。 操作系统使用低功率命令将一个子集或完整的一组事件联结到 NIC。 一些唤醒事件参数的设置比 Dx 命令更早。 其他设置在 Dx 命令之前设置为固件。 所有事件仅通过 Dx 命令启用。

在此接口中，将设置为 "已启用" 的事件在可选的 WDI tlv 中被查明，这会将 [**\_ \_ \_ 唤醒 \_ 事件 tlv 启用**](./wdi-tlv-enable-wake-events.md) 为 OID \_ WDI 为 \_ \_ 设备电源状态 Dx 设置电源命令。 如果操作系统不想 arm NIC 来唤醒，则不会存在 TLV。

当固件接收到带有 [**WDI TLV 的 Dx \_ 命令 \_ 启用 \_ 唤醒 \_ 事件**](./wdi-tlv-enable-wake-events.md)时，它可能会在完成 Dx 命令之前检测到唤醒事件。 它应缓冲事件，完成对命令的处理，然后断言唤醒中断。

每个由 Wi-Fi NIC 唤醒的每个唤醒都应该后跟 NIC 唤醒堆栈的原因的唤醒原因。 NIC 通过断言唤醒中断行来唤醒堆栈，该唤醒中断行通常由总线或 ACPI 方法提供服务。 方法唤醒 CPU 和所需的组件来处理唤醒事件，并为堆栈完成 Wi-Fi 等待唤醒 IRP。 随后，操作系统会向驱动程序和固件发出 D0 请求。 此请求是驱动程序的电源 OID，可向固件发送 D0 命令。 固件包含唤醒原因的指示，直到接收并完成 D0 命令。

**注意**  如果 NIC 出于其他原因而收到 D0 命令 (例如，NIC 不会唤醒主机) ，NIC 不应指示唤醒原因。

 

## <a name="no-enabled-wake-events"></a>无启用的唤醒事件


如果没有 [**WDI \_ TLV 启用了 \_ \_ 唤醒 \_ 事件**](./wdi-tlv-enable-wake-events.md) ，则操作系统不需要 nic 就能以较低的电能运行。 Nic 可能已完全关闭电源。 如果已挂起到硬盘驱动器，则 Nic 驱动程序应在恢复时恢复固件上下文。

## <a name="power-state-interaction-and-transition-examples"></a>电源状态交互和转换示例


以下关系图显示了 NIC 的 D0 (D2 或 D3) 之间的转换交互和序列。 在此上下文中，"微型端口" 表示主机或 WDI 兼容的驱动程序。

### <a name="d0-to-dx-armed-to-wake"></a>D0 到 Dx (唤醒) 

![wdi d0 到 dx 的转换](images/wdi-d0-to-dx-armed-to-wake.png)

-   停止 \[ DnIO |UpIO \] ： DnIO 是 (控件和数据) 到较低层的消息。 UpIO 是指向上层的消息。

    -   拒绝来自上述层的新请求 (无法快速) 。
    -   停止从此层开始 IO (除了此 Dx 命令) 。
    -   允许较低层注入需要进入 Dx 的 TXs。
    -   刷新队列。
-   AwaitInflight：正在等待 IO 调用返回，包括正在进行的 DMA。 刷新队列。

-   Dx 为任何非 D0 状态。 对于 SDBus Wi-fi，此为 D2。 对于 PCIe 总线，此为 D3Hot。 固件不得断电。

### <a name="dx-armed-to-wake-to-d0-transition"></a>Dx (可以唤醒) 到 D0 转换

![dx 能够进行 d0 转换](images/wdi-dx-to-d0-armed-to-wake.png)

-   如果 NIC 唤醒，则无法 D3Cold。 固件必须继续在 Dx 中运行。

### <a name="d0-to-d3-not-armed-to-wake-transition"></a>D0 到 D3 (无法唤醒) 转换

![d0 到 d3 未配备转换](images/wdi-d0-to-d3-not-armed.png)

-   停止 \[ DnIO |UpIO \] ： DnIO 是 (控件和数据) 到较低层的消息。 UpIO 是指向上层的消息。

    -   拒绝来自上述层的新请求 (无法快速) 。
    -   停止从此层开始 IO (除了此 Dx 命令) 。
    -   允许较低层注入需要进入 Dx 的 TXs。
    -   刷新队列。
-   AwaitInflight：正在等待 IO 调用返回，包括正在进行的 DMA。 刷新队列。

-   不带 PmParameters 的 D3。 NIC 可能 (D3Cold) 或可能未关闭 (例如，具有 D0 设备) 的共享电源线。

### <a name="dx-not-armed-to-wake-to-d0-transition"></a>Dx (无法唤醒) 到 D0 转换

![dx 不能进行 d0 转换](images/wdi-dx-to-d0-not-armed.png)

-   D2 notArmToWake：保持通电，无需重新初始化。
-   D3 notArmtoWake：可能是热或冷的。 冷要求还原上下文。

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

