---
title: WDI_TLV_P2P_CHANNEL_INDICATE_REASON
description: WDI_TLV_P2P_CHANNEL_INDICATE_REASON 是包含用于发送指示原因 TLV。
ms.assetid: DD746492-82C5-4458-94A2-778F7F0F30B4
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_CHANNEL_INDICATE_REASON 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 54a541a7741c529a2844c41b1189df8dfef3b519
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385706"
---
# <a name="wditlvp2pchannelindicatereason"></a>WDI\_TLV\_P2P\_通道\_指示\_原因


WDI\_TLV\_P2P\_通道\_指示\_原因是包含用于发送指示原因 TLV。

## <a name="tlv-type"></a>TLV 类型


0x102

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                         |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 用于发送指示原因。 请参阅[ **WDI\_P2P\_通道\_指示\_原因**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_channel_indicate_reason)有关可能的原因。 |

 

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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




