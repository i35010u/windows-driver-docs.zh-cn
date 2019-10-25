---
title: WDI_TLV_UNICAST_ALGORITHM_LIST
description: WDI_TLV_UNICAST_ALGORITHM_LIST 是一个 TLV，其中包含单播数据算法对的数组。
ms.assetid: E216BE6A-5425-498F-ABDE-1229170DA5DB
ms.date: 07/18/2017
keywords:
- WDI_TLV_UNICAST_ALGORITHM_LIST 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0614e6502e48b3e9a8c36b956a8724644783a577
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841721"
---
# <a name="wdi_tlv_unicast_algorithm_list"></a>WDI\_TLV\_单播\_算法\_列表


WDI\_TLV\_单播\_算法\_列表是包含单播数据算法对的数组的 TLV。

## <a name="tlv-type"></a>TLV 类型


0x13

## <a name="length"></a>长度


WDI 的数组的大小（以字节为单位）\_算法\_对元素。 数组必须包含1个或多个元素。

**请注意**  WDI\_算法\_对不是 WDI 结构。 它在 WDI TLV 分析程序生成器中定义，仅用于文档目的。

 

## <a name="values"></a>值


| 在任务栏的搜索框中键入                 | 描述                                            |
|----------------------|--------------------------------------------------------|
| WDI\_算法\_对\[\] | 身份验证和密码算法对的数组。 |

 

WDI\_算法\_对包含以下元素。

| 在任务栏的搜索框中键入  | 描述                                                                                     |
|-------|-------------------------------------------------------------------------------------------------|
| UINT8 | WDI 中定义的身份验证算法[ **\_AUTH\_算法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm)。 |
| UINT8 | 在 WDI 中定义的密码算法[ **\_密码\_算法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)。     |

 

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
<td><p>Windows 10</p></td>
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

 

 




