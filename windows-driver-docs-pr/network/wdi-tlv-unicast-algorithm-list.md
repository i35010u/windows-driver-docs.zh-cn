---
title: WDI_TLV_UNICAST_ALGORITHM_LIST
description: WDI_TLV_UNICAST_ALGORITHM_LIST 是包含单播数据算法对的数组的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_UNICAST_ALGORITHM_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1cee3a69f74638e82d1df9a2feefdf5210be4820
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834133"
---
# <a name="wdi_tlv_unicast_algorithm_list"></a>WDI \_ TLV \_ 单播 \_ 算法 \_ 列表


WDI \_ tlv \_ 单播 \_ 算法 \_ 列表是一个 tlv，其中包含单播数据算法对的数组。

## <a name="tlv-type"></a>TLV 类型


0x13

## <a name="length"></a>长度


WDI \_ 算法对元素数组的大小 (以字节为单位) \_ 。 数组必须包含1个或多个元素。

**注意**  WDI \_ 算法 \_ 对不是 WDI 结构。 它在 WDI TLV 分析程序生成器中定义，仅用于文档目的。

 

## <a name="values"></a>值


| 类型                 | 描述                                            |
|----------------------|--------------------------------------------------------|
| WDI \_ 算法 \_ 对\[\] | 身份验证和密码算法对的数组。 |

 

WDI \_ 算法 \_ 对由下列元素组成。

| 类型  | 描述                                                                                     |
|-------|-------------------------------------------------------------------------------------------------|
| UINT8 | [**WDI \_ AUTH \_ 算法**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm)中定义的身份验证算法。 |
| UINT8 | 在 [**WDI \_ 密码 \_ 算法**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)中定义的密码算法。     |

 

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

 

