---
title: NDIS_STATUS_WDI_INDICATION_NLO_DISCOVERY
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_NLO_DISCOVERY 指示网络列表卸载 (NLO) 发现。
ms.assetid: 1a789bd8-8601-45f3-a9bf-5220c20379cb
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_NLO_DISCOVERY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: deab9e17b1009b1e72dbfd4d849b70e3f185a053
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390674"
---
# <a name="ndisstatuswdiindicationnlodiscovery"></a>NDIS\_状态\_WDI\_指示\_NLO\_发现


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_NLO\_发现，以指示网络列表卸载 (NLO) 发现。

| Object |
|--------|
| 端口   |

 

固件检测 APs NLO 中向下推送的 Ssid。 NLO 用在非 AOAC 系统的快速连接，从系统睡眠状态恢复时。 它还用于在 AOAC 系统中扫描 APs 推送到固件的 Ssid。

操作系统不要求在 CS 中扫描周期性后台操作。 NLO 扫描是 CS 中的首选的方法因为屏幕处于关闭状态时用户不需要查看所有可见的 Ap，但这些用户具有的 Ssid 为自动连接配置文件，以自动连接到。 Ssid 来卸载从操作系统列表中有一个首选的身份验证和密码对和最多 4 个通道提示。 如果列表中有至少一个 SSID，固件应启动自动遵循的计划快速扫描和进行慢扫描阶段未 NLO 扫描。 在类驱动程序将转换为对固件请求的 OS 请求。 固件应进行 NLO 扫描根据 APs 支持首选的身份验证和密码对与 Ssid 相关联的计划。

在每个扫描期间，固件扫描与条件匹配的列表，但不是必要的通道上的通道列表受约束的 Ssid。 应为可能缓存的已发现的接入点信息。

如果找到任何匹配项，固件指示 NLO 发现和缓存主机检索发现的接入点信息的列表。

在以下两种情况中发生的 NLO 发现指示。

-   当 NIC 为 Dx 中：
    1.  触发唤醒中断并等待集幂 D0 继续以下步骤。
    2.  指示 NLO 发现。
    3.  指示固件唤醒原因为 NLO 发现堆栈。
-   当 NIC 为 D0:
    -   指示 NLO 发现。

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                   | 允许多个 TLV 实例 | 可选 | 描述                                                                                      |
|--------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_BSS\_ENTRY**](https://msdn.microsoft.com/library/windows/hardware/dn926162) | X                              |          | BSSIDs 的列表。 该列表必须至少包含触发此发现状态的项。 |

 

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

 

 




