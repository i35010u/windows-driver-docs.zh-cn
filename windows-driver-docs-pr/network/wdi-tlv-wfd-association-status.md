---
title: WDI_TLV_WFD_ASSOCIATION_STATUS
description: WDI_TLV_WFD_ASSOCIATION_STATUS 是一种 TLV，其中包含在拒绝关联请求时要设置的状态代码。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_WFD_ASSOCIATION_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 04569402d2b043e857918557843c82ddc58c42ee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834101"
---
# <a name="wdi_tlv_wfd_association_status"></a>WDI \_ TLV \_ WFD \_ 关联 \_ 状态


WDI \_ tlv \_ WFD \_ 关联 \_ 状态是一个 TLV，其中包含在拒绝关联请求时要设置的状态代码。

## <a name="tlv-type"></a>TLV 类型


0x126

## <a name="length"></a>长度


UINT8 的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型  | 描述                                                                   |
|-------|-------------------------------------------------------------------------------|
| UINT8 | \_ \_ \_ 拒绝关联请求时要设置的 DOT11 WFD 状态代码。 |

 

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

 

 




