---
title: WDI_TLV_CHANNEL_LIST
description: WDI_TLV_CHANNEL_LIST 是包含一个或多个通道号的 TLV。
ms.assetid: DBBA28C2-D80F-409B-BEE6-81B6FEDF7484
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CHANNEL_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c3f592aa2e52ee899c72b694532ee929b07b9dee
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209615"
---
# <a name="wdi_tlv_channel_list"></a>WDI \_ TLV \_ 通道 \_ 列表


WDI \_ tlv \_ 通道 \_ 列表是包含一个或多个通道号的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x4

## <a name="length"></a>Length


[**WDI \_ 信道 \_ 映射 \_ 条目**](/windows-hardware/drivers/ddi/wditypes/ns-wditypes-_wdi_channel_mapping_entry)结构数组的大小 (以字节为单位) 。 数组必须包含1个或多个结构。

## <a name="values"></a>值


| 类型                                                                       | 说明                          |
|----------------------------------------------------------------------------|--------------------------------------|
| [**WDI \_ 通道 \_ 映射 \_ 条目**](/windows-hardware/drivers/ddi/wditypes/ns-wditypes-_wdi_channel_mapping_entry)\[\] | 通道映射项的数组。 |

 

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

 

