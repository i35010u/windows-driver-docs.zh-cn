---
title: WDI_TLV_CONNECTION_QUALITY_PARAMETERS
description: WDI_TLV_CONNECTION_QUALITY_PARAMETERS 是包含所需 Wi-Fi 连接质量提示的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CONNECTION_QUALITY_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9878fd7d6a2cf47018452f5f99061716742f66a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822737"
---
# <a name="wdi_tlv_connection_quality_parameters"></a>WDI \_ TLV \_ 连接 \_ 质量 \_ 参数


WDI \_ tlv \_ 连接 \_ 质量 \_ 参数是一个 tlv，其中包含所需的 Wi-Fi 连接质量提示。

## <a name="tlv-type"></a>TLV 类型


0xA3

## <a name="length"></a>长度


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 描述                                                                                                                          |
|--------|--------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 所需的 Wi-Fi 连接质量提示，如 [**WDI \_ 连接 \_ 质量 \_ 提示**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_connection_quality_hint)中所定义。 |

 

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

 

