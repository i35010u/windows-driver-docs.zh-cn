---
title: NDIS_STATUS_WDI_INDICATION_NLO_DISCOVERY
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_NLO_DISCOVERY 指示网络列表卸载 (NLO) 发现。
ms.assetid: 1a789bd8-8601-45f3-a9bf-5220c20379cb
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_NLO_DISCOVERY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fa77a642999477080b5b4f917def9bb18f31f870
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209705"
---
# <a name="ndis_status_wdi_indication_nlo_discovery"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ NLO \_ 发现


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI \_ 指示 \_ NLO \_ 发现来指示 (NLO) 发现的网络列表卸载。

| 对象 |
|--------|
| 端口   |

 

该固件检测 NLO 中推送的 Ssid 的 Ap。 当从系统睡眠恢复时，NLO 在非 AOAC 系统中用于快速连接。 它还在 AOAC 系统中用于扫描推送到固件的 Ssid 的 Ap。

当在 CS 中时，OS 不会请求定期后台扫描。 NLO 扫描是 CS 中首选的方法，因为用户无需查看所有可见的 Ap，而是用户具有自动连接配置文件自动连接到的 Ssid 时，屏幕是关闭的。 要从操作系统中卸载的 Ssid 列表具有首选的身份验证和密码对以及最多4个通道提示。 当列表中至少有一个 SSID 时，固件会按照快速扫描和慢速扫描阶段的计划自行启动 NLO 扫描。 类驱动程序将操作系统请求转换为固件请求。 此固件应根据支持与 Ssid 关联的首选身份验证和密码对的 Ap 计划进行 NLO 扫描。

在每个扫描周期内，固件会扫描与通道列表上的条件匹配但不需要在通道列表中进行约束的 Ssid。 应缓存发现的 AP 信息以指示。

找到任何匹配项后，固件将指示 NLO 发现，并缓存已发现的用于要检索的主机的 AP 信息的列表。

在以下两种情况下，NLO 发现的指示发生。

-   如果 NIC 位于 Dx 中：
    1.  触发唤醒中断并等待将电源设置为 D0 以继续执行以下步骤。
    2.  指示 NLO 发现。
    3.  指示固件将堆栈唤醒，原因是 NLO 发现。
-   如果 NIC 为 D0：
    -   指示 NLO 发现。

## <a name="payload-data"></a>负载数据


| 类型                                                   | 允许多个 TLV 实例 | 可选 | 说明                                                                                      |
|--------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ BSS \_ 条目**](./wdi-tlv-bss-entry.md) | X                              |          | BSSIDs 的列表。 此列表必须至少包含触发此发现状态的条目。 |

 

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
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

