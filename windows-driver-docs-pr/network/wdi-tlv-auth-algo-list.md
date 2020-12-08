---
title: WDI_TLV_AUTH_ALGO_LIST
description: WDI_TLV_AUTH_ALGO_LIST 为 TLV，其中包含身份验证算法的列表。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_AUTH_ALGO_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d18b8028e68547724974932c48b2c5abfaa7d30c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832087"
---
# <a name="wdi_tlv_auth_algo_list"></a>WDI \_ TLV \_ 身份验证 \_ 算法 \_ 列表


WDI \_ tlv \_ \_ authentication 算法 \_ list 是包含一系列身份验证算法的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x3C

## <a name="length"></a>长度


[**WDI \_ AUTH \_ 算法**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm)结构数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型                                                        | 描述                            |
|-------------------------------------------------------------|----------------------------------------|
| [**WDI \_ AUTH \_ 算法**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm)\[\] | 身份验证算法的数组。 |

 

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

 

