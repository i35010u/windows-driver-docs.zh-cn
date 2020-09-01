---
title: WDI_TLV_ETHERTYPE_ENCAP_TABLE
description: WDI_TLV_ETHERTYPE_ENCAP_TABLE 为 TLV，其中包含关联的 Ethertype 封装。
ms.assetid: BAAC7E5B-F13F-4AC8-A3F9-76197F92C7E3
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ETHERTYPE_ENCAP_TABLE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 576c5654cd283649bfb1f959503b88cc4f2a4010
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217215"
---
# <a name="wdi_tlv_ethertype_encap_table"></a>WDI \_ TLV \_ ETHERTYPE \_ ENCAP \_ 表


WDI \_ TLV \_ ETHERTYPE \_ ENCAP \_ 表是一个 tlv，其中包含关联的 ETHERTYPE 封装。

## <a name="tlv-type"></a>TLV 类型


0x31

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                                                                       | 说明                                                                                                                                                                  |
|--------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ ETHERTYPE \_ 封装 \_ 项**](/windows-hardware/drivers/ddi/wditypes/ns-wditypes-_wdi_ethertype_encapsulation_entry)\[\] | [**WDI \_ ETHERTYPE \_ 封装 \_ 项**](/windows-hardware/drivers/ddi/wditypes/ns-wditypes-_wdi_ethertype_encapsulation_entry)元素的数组，用于指定关联的 ETHERTYPE 封装。 |

 

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

 

