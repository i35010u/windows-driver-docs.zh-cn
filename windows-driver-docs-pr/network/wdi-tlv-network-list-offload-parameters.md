---
title: WDI_TLV_NETWORK_LIST_OFFLOAD_PARAMETERS
description: WDI_TLV_NETWORK_LIST_OFFLOAD_PARAMETERS 是一种 TLV，其中包含用于 OID_WDI_SET_NETWORK_LIST_OFFLOAD 的网络列表卸载 (NLO) 参数。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_NETWORK_LIST_OFFLOAD_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 21e188342b8f48387485391ce7522e0153169ccb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821218"
---
# <a name="wdi_tlv_network_list_offload_parameters"></a>WDI \_ TLV \_ 网络 \_ 列表 \_ 卸载 \_ 参数


WDI \_ tlv \_ 网络 \_ 列表 \_ 卸载 \_ 参数是一个 TLV，其中包含用于 [OID \_ WDI \_ SET \_ network \_ list \_ 卸载](./oid-wdi-set-network-list-offload.md)的网络列表卸载 (NLO) 参数。

## <a name="tlv-type"></a>TLV 类型


0x59

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                    | 允许多个 TLV 实例 | 可选 | 说明                                                                                  |
|-----------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 网络 \_ 列表 \_ 卸载 \_ 配置**](wdi-tlv-network-list-offload-config.md) |                                |          | 指定 NLO 配置。                                                                 |
| [**WDI \_ TLV \_ SSID \_ 卸载**](wdi-tlv-ssid-offload.md)                                 | X                              | X        | 指定卸载 Ssid。 如果此元素不存在，固件应停止 NLO 扫描。 |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

