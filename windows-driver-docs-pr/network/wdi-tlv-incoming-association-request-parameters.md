---
title: WDI_TLV_INCOMING_ASSOCIATION_REQUEST_PARAMETERS
description: WDI_TLV_INCOMING_ASSOCIATION_REQUEST_PARAMETERS 是包含关联请求参数的 TLV。
ms.assetid: DC3439A2-2221-4489-AB38-3752624EA4B2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INCOMING_ASSOCIATION_REQUEST_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3e4a9e3b4a2c39a39da1fe29c50a2aecaede9e23
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206711"
---
# <a name="wdi_tlv_incoming_association_request_parameters"></a>WDI \_ TLV \_ 传入 \_ 关联 \_ 请求 \_ 参数


WDI \_ tlv \_ 传入 \_ 关联 \_ 请求 \_ 参数是包含关联请求参数的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x7D

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                              | 说明                                                                                                                   |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 发件人的 MAC 地址。                                                                                                |
| UINT8                                             | 一个指示它是否为重新关联请求的位。 如果值为1，则表示它是一个重新关联请求。 |

 

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

 

