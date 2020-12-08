---
title: WDI_TLV_ACTION_FRAME_BODY
description: WDI_TLV_ACTION_FRAME_BODY 是包含操作框正文的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ACTION_FRAME_BODY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 492c885d8182a43d245de0f1805451c7d54f8da7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822051"
---
# <a name="wdi_tlv_action_frame_body"></a>WDI \_ TLV \_ 操作 \_ 框架 \_ 正文


WDI \_ tlv \_ 操作 \_ 框架 \_ 正文是包含操作帧正文的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xBE

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                           |
|-----------|-----------------------------------------------------------------------|
| UINT8\[\] | 包含操作框正文的 UINT8 元素的数组。 |

 

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

 

 




