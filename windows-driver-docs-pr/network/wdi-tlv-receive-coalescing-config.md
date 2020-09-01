---
title: WDI_TLV_RECEIVE_COALESCING_CONFIG
description: WDI_TLV_RECEIVE_COALESCING_CONFIG 是包含接收合并配置的 TLV。
ms.assetid: 32542203-14DE-4F91-AB85-D2FA75ECAB9E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_RECEIVE_COALESCING_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b67161b32346e367a8cf79399fa5f284818cd371
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218292"
---
# <a name="wdi_tlv_receive_coalescing_config"></a>WDI \_ TLV \_ 接收 \_ 合并 \_ 配置


WDI \_ tlv \_ 接收 \_ 合并 \_ 配置是包含接收合并配置的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xDB

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型   | 说明                                                         |
|--------|---------------------------------------------------------------------|
| UINT32 | 与此筛选器匹配的队列数据包的唯一队列 ID。            |
| UINT32 | 值介于1与支持的筛选器数之间的筛选器 ID。 |
| UINT32 | 最大合并延迟（毫秒）。                       |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID \_ WDI \_ 设置 \_ 接收 \_ 合并](./oid-wdi-set-receive-coalescing.md)

 

