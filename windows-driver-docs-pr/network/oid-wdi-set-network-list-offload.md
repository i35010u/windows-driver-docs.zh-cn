---
title: OID_WDI_SET_NETWORK_LIST_OFFLOAD
description: OID_WDI_SET_NETWORK_LIST_OFFLOAD 设置固件扫描的 Ap 首选 Ssid 的列表。
ms.assetid: 2df9ee2b-78df-4f92-9b40-5945ecc81c7e
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_NETWORK_LIST_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a4054848f7df650f19e89d4912704f53d97d797f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534071"
---
# <a name="oidwdisetnetworklistoffload"></a>OID\_WDI\_SET\_NETWORK\_LIST\_OFFLOAD


OID\_WDI\_设置\_网络\_列表\_卸载设置固件扫描的 Ap 首选 Ssid 的列表。

| 范围        | 设置与任务序列化 | 正常执行时间 （秒） |
|--------------|--------------------------|---------------------------------|
| 主端口 | 是                      | 1                               |

 

有两种类型的网络列表卸载 (NLO)。 一个类型为始终上始终连接 (AOAC) 系统上的卸载到 Nic。 另一个是即时连接 NLO 的 Windows 8 和 Windows 8.1 中仅用于非 AOAC 系统快速在从休眠恢复时重新连接的 Wi-fi。 对于即时连接列表之前系统进入休眠状态发送。 今后，即时连接用于 resume 从支持它的 AOAC 系统上的休眠状态。

## <a name="instant-connect"></a>即时连接


WDI 处理即时连接 NLO，并使用有针对性的扫描的组合来满足从 OS 请求。 IHV 驱动程序不需要处理此连接的即时 OS 请求。

当从休眠中恢复操作系统时，操作系统将发送即时连接 NLO。 WDI 可以扫描 OID 为目标的所有通道提示的联合。 IHV 驱动程序应支持此类中定义目标一次扫描[OID\_WDI\_任务\_扫描](oid-wdi-task-scan.md)。 以下部分适用于网络卸载到 AOAC 系统上支持的 Nic 的列表。

## <a name="network-list-offload"></a>卸载功能的网络列表


操作系统不要求在 CS 中扫描周期性后台操作。 NLO 扫描是 CS 中的首选的方法，因为用户不需要以查看所有可见 Ap 时，屏幕处于关闭状态。 用户具有的 Ssid 自动连接配置文件设置为自动连接是唯一的有用 APs。 Ssid 来卸载与操作系统的列表不包含首选的身份验证和密码对，和多达四个通道的提示。 当列表中包含至少一个 SSID 时，固件应开始进行 NLO 扫描自主，关注的快速扫描和进行慢扫描阶段的计划。 WDI 兼容的驱动程序将对固件请求操作系统请求。 应在固件 NLO 扫描根据 Ap 的计划。 APs 应支持的首选身份验证和密码对与 Ssid 相关联。

对固件请求具有通道提示的列表，对于所有卸载 Ssid。 WDI 兼容的驱动程序将它们合并的固件。 例如，如果 SSID1\[auth1，cipher1\]具有通道提示的 1 和 6 和 SSID2\[auth2，cipher2\]通道提示 6 和 11，对固件的请求是一系列 Ssid {SSID1\[auth1，cipher1\]，SSID2\[auth2，cipher2\] } 和频道扫描 {1、 6、 11} 列表。

在每个扫描期间，固件将扫描的匹配列表的通道，但并不是必需的条件约束上的通道列表的 Ssid。 应缓存要检索的主机的发现的接入点信息。 固件指示 NLO 发现时至少一个 BSSID 匹配 SSID、 算法和加密算法，但通道匹配不需要。

每个 OID\_WDI\_设置\_网络\_列表\_UE 将发送到 LE 卸载表示的最新的 NLO 扫描请求。 任何以前续订此类请求或状态。 LE NLO 扫描，并仅指示为每个请求找到 AP 的一次。 UE replumbs （12 倍; 这是可能发生变更） 在 Dx NLO 转换，如果找到的 AP 未成功连接 (如原因： 找到 AP，但设备移动，AP 信号淡化，并且连接将失败; 或延长 EAP 身份验证会失败仅通过）。 LE 和固件应延迟 NLO 扫描计划根据中的延迟配置[ **WDI\_TLV\_网络\_列表\_卸载\_配置**](https://msdn.microsoft.com/library/windows/hardware/dn897851). 这是用户设备使用符合操作系统的原始 NLO 命令的计划数。

NLO 默认扫描类型是 WDI\_扫描\_类型\_自动。 当主动扫描一个通道，固件应使用通配符 SSID。 可见 APs 应与 Ssid 上卸载列表来确定匹配项进行比较。 这是为了降低隐私风险。

指示 NLO 发现有两种情况。

1.  D2 NIC 时，它必须执行以下步骤。
    -   触发器唤醒中断和继续执行以下步骤之前，等待集 D0 幂。
    -   指示固件唤醒原因为 NLO 发现堆栈。
    -   返回 D0 命令。
    -   指示 NLO 发现所有找到的接入点信息。

2.  D0 NIC 时，它必须执行以下步骤。
    -   指示 NLO 发现所有找到的接入点信息。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                                  | 允许多个 TLV 实例 | 可选 | 描述         |
|------------------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------|
| [**WDI\_TLV\_NETWORK\_LIST\_OFFLOAD\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/dn897852) |                                |          | NLO 参数中。 |

 

## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。
要求
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
<td><p>标头</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




