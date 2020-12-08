---
title: WDI_TLV_CHANNEL_INFO_LIST
description: WDI_TLV_CHANNEL_INFO_LIST 是包含通道列表的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CHANNEL_INFO_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 36e94182ce26ffaa4b2fd97a862ed67f32e4a4bd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827457"
---
# <a name="wdi_tlv_channel_info_list"></a>WDI \_ TLV \_ 通道 \_ 信息 \_ 列表


WDI \_ tlv \_ 通道 \_ 信息 \_ 列表是包含通道列表的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x41

## <a name="length"></a>长度


WDI 信道号)  (数组的大小（以字节为单位）， \_ \_ (UINT32) 结构。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型       | 描述                 |
|------------|-----------------------------|
| UINT32\[\] | Wi-Fi 通道的数组。 |

 

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

 

 




