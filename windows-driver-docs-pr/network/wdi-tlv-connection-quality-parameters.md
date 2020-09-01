---
title: WDI_TLV_CONNECTION_QUALITY_PARAMETERS
description: WDI_TLV_CONNECTION_QUALITY_PARAMETERS 是包含所需 Wi-fi 连接质量提示的 TLV。
ms.assetid: A371FD3A-5BF9-4921-AB8E-1651789FA9A1
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CONNECTION_QUALITY_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ec044b7382cefb4847ba75eb2cf22fefcb7e7996
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210043"
---
# <a name="wdi_tlv_connection_quality_parameters"></a>WDI \_ TLV \_ 连接 \_ 质量 \_ 参数


WDI \_ tlv \_ 连接 \_ 质量 \_ 参数是一个 tlv，其中包含所需的 wi-fi 连接质量提示。

## <a name="tlv-type"></a>TLV 类型


0xA3

## <a name="length"></a>Length


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 说明                                                                                                                          |
|--------|--------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | [**WDI \_ 连接 \_ 质量 \_ 提示**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_connection_quality_hint)中定义的所需 wi-fi 连接质量提示。 |

 

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

 

