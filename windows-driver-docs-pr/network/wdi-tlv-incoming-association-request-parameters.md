---
title: WDI_TLV_INCOMING_ASSOCIATION_REQUEST_PARAMETERS
description: WDI_TLV_INCOMING_ASSOCIATION_REQUEST_PARAMETERS 是包含关联请求参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INCOMING_ASSOCIATION_REQUEST_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: da8bfcac5c2677d27cc0a8644f717e7d4c9c7295
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837087"
---
# <a name="wdi_tlv_incoming_association_request_parameters"></a>WDI \_ TLV \_ 传入 \_ 关联 \_ 请求 \_ 参数


WDI \_ tlv \_ 传入 \_ 关联 \_ 请求 \_ 参数是包含关联请求参数的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x7D

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                              | 描述                                                                                                                   |
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

