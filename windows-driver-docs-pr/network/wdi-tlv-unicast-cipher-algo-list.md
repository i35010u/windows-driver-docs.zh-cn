---
title: WDI_TLV_UNICAST_CIPHER_ALGO_LIST
description: WDI_TLV_UNICAST_CIPHER_ALGO_LIST 是包含单播密码算法列表的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_UNICAST_CIPHER_ALGO_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ba6743ef3427428457a810966a65a148590491be
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821953"
---
# <a name="wdi_tlv_unicast_cipher_algo_list"></a>WDI \_ TLV \_ 单播 \_ 密码 \_ 算法 \_ 列表


WDI \_ tlv \_ 单播 \_ 密码 \_ 算法 \_ 列表是包含单播密码算法列表的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x3E

## <a name="length"></a>长度


[**WDI \_ 密码 \_ 算法**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)结构数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型                                                            | 描述                            |
|-----------------------------------------------------------------|----------------------------------------|
| [**WDI \_ 密码 \_ 算法**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)\[\] | 单播密码算法的数组。 |

 

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

 

