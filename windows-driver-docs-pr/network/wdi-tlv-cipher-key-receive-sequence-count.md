---
title: WDI_TLV_CIPHER_KEY_RECEIVE_SEQUENCE_COUNT
description: WDI_TLV_CIPHER_KEY_RECEIVE_SEQUENCE_COUNT 是包含接收序列计数 TLV。
ms.assetid: 29AA9D90-834F-4043-B12A-87705EDC1DF0
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_RECEIVE_SEQUENCE_COUNT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 076e34f0acff9e671bd3582ee58df8d269d96b99
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568918"
---
# <a name="wditlvcipherkeyreceivesequencecount"></a>WDI\_TLV\_CIPHER\_KEY\_RECEIVE\_SEQUENCE\_COUNT


WDI\_TLV\_密码\_密钥\_接收\_序列\_计数是包含接收序列计数 TLV。

## <a name="tlv-type"></a>TLV 类型


0x4F

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入       | 描述                                                                                    |
|------------|------------------------------------------------------------------------------------------------|
| UINT8\[6\] | 指定初始 48 位值的数据包数 (PN)，用于进行重播保护。 |

 

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

 

 




