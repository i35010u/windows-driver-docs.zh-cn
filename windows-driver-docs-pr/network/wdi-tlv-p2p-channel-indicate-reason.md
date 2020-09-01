---
title: WDI_TLV_P2P_CHANNEL_INDICATE_REASON
description: WDI_TLV_P2P_CHANNEL_INDICATE_REASON 是一种 TLV，其中包含发送指示的原因。
ms.assetid: DD746492-82C5-4458-94A2-778F7F0F30B4
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_CHANNEL_INDICATE_REASON 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6bdb1935cb1fe5a424765eb0f184f1a2ca4262ef
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217479"
---
# <a name="wdi_tlv_p2p_channel_indicate_reason"></a>WDI \_ TLV \_ P2P \_ 通道 \_ 指示 \_ 原因


WDI \_ TLV \_ P2P \_ 通道 \_ 指示 \_ 原因是包含发送指示的原因的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x102

## <a name="length"></a>Length


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 说明                                                                                                                                         |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 发送指示的原因。 请参阅 [**WDI \_ P2P \_ 通道 \_ 指明 \_ 原因原因**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_channel_indicate_reason) 。 |

 

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

 

