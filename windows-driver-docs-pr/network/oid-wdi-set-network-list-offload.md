---
title: OID_WDI_SET_NETWORK_LIST_OFFLOAD
description: OID_WDI_SET_NETWORK_LIST_OFFLOAD 设置固件的首选 Ssid 列表，以扫描 Ap。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_NETWORK_LIST_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 686f063c6062ecb3a6bb22cff4a3987763447134
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829363"
---
# <a name="oid_wdi_set_network_list_offload"></a>OID \_ WDI \_ SET \_ 网络 \_ 列表 \_ 卸载


OID \_ WDI \_ SET \_ 网络 \_ 列表 \_ 卸载设置用于扫描 Ap 的固件的首选 ssid 列表。

| 范围        | 设置序列化任务 | 正常执行时间 (秒)  |
|--------------|--------------------------|---------------------------------|
| 主端口 | 是                      | 1                               |

 

有两种类型的网络列表卸载 (NLO) 。 一种类型会卸载到 Always On 始终连接 (AOAC) 系统上的 Nic。 另一种是即时连接 NLO，在 Windows 8 和 Windows 8.1 中，仅用于非 AOAC 系统，以便在从休眠状态恢复时快速重新连接 Wi-Fi。 对于 "即时连接"，将在系统进入休眠状态之前发送列表。 接下来，即时连接用于在支持它的 AOAC 系统上从休眠中恢复。

## <a name="instant-connect"></a>即时连接


WDI 处理即时连接 NLO，并使用目标扫描的组合来完成来自 OS 的请求。 IHV 驱动程序无需处理此即时连接操作系统请求。

当 OS 从休眠恢复时，操作系统将发送即时连接 NLO。 WDI 为目标扫描 OID 建立所有通道提示的联合。 IHV 驱动程序应支持在 [OID \_ WDI \_ 任务 \_ 扫描](oid-wdi-task-scan.md)中定义的此类目标扫描。 以下部分适用于 AOAC 系统上支持的 Nic 的网络列表卸载。

## <a name="network-list-offload"></a>网络列表卸载


当在 CS 中时，OS 不会请求定期后台扫描。 NLO 扫描是 CS 中首选的方法，因为用户无需查看所有可见的 Ap 时，屏幕是关闭的。 用户将自动连接配置文件设置为自动连接的 Ssid 是唯一有用的 Ap。 要从操作系统中卸载的 Ssid 列表具有首选的身份验证和密码对以及最多四个通道提示。 当列表中至少有一个 SSID 时，固件会按照快速扫描和慢速扫描阶段的计划，自行开始进行 NLO 扫描。 WDI 兼容驱动程序将操作系统请求转换为固件请求。 固件应根据 Ap 的计划进行 NLO 扫描。 Ap 应支持与 Ssid 关联的首选身份验证和密码对。

向固件发出的请求包含所有卸载 Ssid 的通道提示列表。 与 WDI 兼容的驱动程序将其与固件组合在一起。 例如，如果 SSID1 \[ auth1，cipher1 的 \] 通道提示为1和6，SSID2 \[ auth2，cipher2 的 \] 通道提示为6和11，则对固件的请求是 ssid {SSID1 \[ auth1，cipher1 \] ，SSID2 \[ auth2，cipher2 \] } 和要扫描的通道列表 {1，6，11} 的列表。

在每个扫描周期内，固件会扫描与通道列表上的条件匹配的 Ssid，但不需要对通道列表进行约束。 应为要检索的主机缓存发现的 AP 信息。 当至少有一个 BSSID 匹配 SSID、算法和密码时，固件指示 NLO 发现，但不需要通道匹配。

每个 OID \_ WDI \_ 设置 \_ 网络 \_ 列表 \_ 卸载，UE 发送到 LE 的网络列表卸载表示一个全新的 NLO 扫描请求。 以前的此类请求或状态将续订。 针对每个请求的找到的 AP，NLO 的 LE 扫描仅指示一次。 UE replumbs (12 次;如果由于如下原因 (找到的 AP 未成功连接，则这可能会改变 Dx 转换) NLO：找到接入点，但设备会四处移动，而 AP 信号会淡化，连接将会失败;或通过) 来延长 EAP 身份验证失败时发生。 根据 [**WDI \_ TLV \_ 网络 \_ 列表 \_ 卸载 \_ 配置**](./wdi-tlv-network-list-offload-config.md)中的延迟配置，LE 和固件应延迟 NLO 扫描计划。 这是一个数字，UE 使用它来符合操作系统的原始 NLO 命令的计划。

NLO 的默认扫描类型为 WDI \_ scan \_ type \_ AUTO。 主动扫描通道时，固件应使用通配符 SSID。 应将可见的 Ap 与卸载列表中的 Ssid 进行比较以确定是否匹配。 这是为了减少隐私曝光。

指示 NLO 发现有两种情况。

1.  如果 NIC 在 D2 中，则必须执行以下步骤。
    -   触发唤醒中断并等待将电源设置为 D0，然后继续执行以下步骤。
    -   指示固件将堆栈唤醒，原因是 NLO 发现。
    -   返回 D0 命令。
    -   用所有找到的 AP 信息指示 NLO 发现。

2.  如果 NIC 为 D0，则必须执行以下步骤。
    -   用所有找到的 AP 信息指示 NLO 发现。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                                  | 允许多个 TLV 实例 | 可选 | 说明         |
|------------------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------|
| [**WDI \_ TLV \_ 网络 \_ 列表 \_ 卸载 \_ 参数**](./wdi-tlv-network-list-offload-parameters.md) |                                |          | NLO 参数。 |

 

## <a name="set-property-results"></a>设置属性结果


无其他数据。 标头中的数据足够了。

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

 

