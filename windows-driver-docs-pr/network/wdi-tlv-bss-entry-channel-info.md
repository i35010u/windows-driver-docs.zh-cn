---
title: WDI_TLV_BSS_ENTRY_CHANNEL_INFO
description: WDI_TLV_BSS_ENTRY_CHANNEL_INFO 是包含 BSS 条目通道信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BSS_ENTRY_CHANNEL_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b86b5e4f65e627005839b43f79178a72956e043b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792609"
---
# <a name="wdi_tlv_bss_entry_channel_info"></a>WDI \_ TLV \_ BSS \_ 条目 \_ 通道 \_ 信息


WDI \_ tlv \_ BSS \_ 条目 \_ 通道 \_ 信息是包含 BSS 条目通道信息的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x3A

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                          | 描述                                                  |
|-------------------------------|--------------------------------------------------------------|
| WDI \_ 信道 \_ 号 (UINT32)  | 在其上发现对等方的逻辑通道号。 |
| UINT32                        | BSS 项的带区 ID。                               |

 

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

 

 




