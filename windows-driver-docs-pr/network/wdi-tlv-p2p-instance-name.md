---
title: WDI_TLV_P2P_INSTANCE_NAME
description: WDI_TLV_P2P_INSTANCE_NAME 为 TLV，其中包含服务的实例名称。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INSTANCE_NAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7547cddeb19f4ce7f270f3461025795cc25adb77
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818241"
---
# <a name="wdi_tlv_p2p_instance_name"></a>WDI \_ TLV \_ P2P \_ 实例 \_ 名称


WDI \_ tlv \_ P2P \_ INSTANCE \_ name 是包含服务的实例名称的 tlv。

**注意**  此 TLV 已添加到 Windows 10 版本1607，WDI 版本1.0.21 中。

 

## <a name="tlv-type"></a>TLV 类型


0x12B

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                     |
|-----------|-----------------------------------------------------------------|
| UINT8\[\] | UTF-8 中服务的实例名称，长度最大为63个字节。 |

 

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

 

 




