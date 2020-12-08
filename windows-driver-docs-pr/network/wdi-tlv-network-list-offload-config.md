---
title: WDI_TLV_NETWORK_LIST_OFFLOAD_CONFIG
description: WDI_TLV_NETWORK_LIST_OFFLOAD_CONFIG 是一种 TLV，其中包含 (NLO) 配置的网络列表卸载。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_NETWORK_LIST_OFFLOAD_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9f3923b0a838a72f821908c15f83d87d956386ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788255"
---
# <a name="wdi_tlv_network_list_offload_config"></a>WDI \_ TLV \_ 网络 \_ 列表 \_ 卸载 \_ 配置


WDI \_ tlv \_ 网络 \_ 列表 \_ 卸载 \_ 配置是一个 Tlv，其中包含的网络列表卸载 (NLO) 配置。

## <a name="tlv-type"></a>TLV 类型


0xDA

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型   | 描述                                                                                                           |
|--------|-----------------------------------------------------------------------------------------------------------------------|
| UINT32 | 保留的字段。                                                                                                       |
| UINT32 | 扫描计划开始之前)  (的延迟时间（秒）。                                                               |
| UINT32 | ) 在第一阶段中进行扫描的时间段 (以秒为单位）。                                                                   |
| UINT32 | 快速扫描阶段中的迭代数。                                                                      |
| UINT32 | 时间段 () 在慢速扫描阶段扫描。 在设置新的 NLO 命令之前，此阶段会无限期地持续下去。 |

 

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

 

 




