---
title: OID_WDI_GET_BSS_ENTRY_LIST
description: OID_WDI_GET_BSS_ENTRY_LIST 用于请求适配器指示已由端口缓存的 BSS 网络的列表。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_GET_BSS_ENTRY_LIST 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e2480f658c16090646c9b79ab5e3bb6b5d438104
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794347"
---
# <a name="oid_wdi_get_bss_entry_list"></a>OID \_ WDI \_ 获取 \_ BSS \_ 条目 \_ 列表


OID \_ WDI \_ 获取 \_ bss \_ 条目 \_ 列表用于请求适配器指示已由端口缓存的 BSS 网络的列表。

| 范围 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 不支持的设置        | 1                               |

 

这仅用于执行 BSS 列表缓存的适配器。 作为客户端时，端口必须报告接入点的 BSS 条目。 此外，如果端口正在执行后台扫描，它应报告在其扫描中发现的 BSS 条目。

当适配器接收到此请求时，它必须将 [NDIS \_ 状态 \_ WDI \_ 指示 \_ BSS \_ 条目 \_ 列表](ndis-status-wdi-indication-bss-entry-list.md) 指示发送到 Microsoft 组件。 这些指示必须包含与 Get 参数匹配的 BSS 条目。 适配器可以发送一个或多个 NDIS \_ 状态 \_ WDI \_ 指示 \_ BSS \_ 条目 \_ 列表指示，但必须在属性完成前完成。

Microsoft 组件使用指示条目的列表将 BSS 列表报告给操作系统。 它还用于填充用于漫游和连接任务的参数。

## <a name="get-property-parameters"></a>获取属性参数


| TLV                                         | 允许多个 TLV 实例 | 可选 | 说明                                           |
|---------------------------------------------|--------------------------------|----------|-------------------------------------------------------|
| [**WDI \_ TLV \_ SSID**](./wdi-tlv-ssid.md) |                                |          | 主机需要对其进行 BSS 列表更新的 SSID。 |

 

## <a name="get-property-results"></a>获取属性结果


无其他数据。 标头中的数据足够了。
## <a name="unsolicited-indication"></a>未经请求的指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ BSS \_ 条目 \_ 列表](ndis-status-wdi-indication-bss-entry-list.md)

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

 

