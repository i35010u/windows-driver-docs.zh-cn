---
title: WDI_TLV_UNICAST_CIPHER_ALGO_LIST
description: WDI_TLV_UNICAST_CIPHER_ALGO_LIST 是包含一系列单播密码算法 TLV。
ms.assetid: 67FAEE8A-1CD6-4430-92C1-84E9F43BEF63
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_UNICAST_CIPHER_ALGO_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1c164db319b3f8aff3fed9f80c71f08c39254cd0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366901"
---
# <a name="wditlvunicastcipheralgolist"></a>WDI\_TLV\_UNICAST\_CIPHER\_ALGO\_LIST


WDI\_TLV\_单播\_密码\_ALGO\_列表是包含一系列单播密码算法 TLV。

## <a name="tlv-type"></a>TLV 类型


0x3E

## <a name="length"></a>长度


数组的大小 （以字节为单位） [ **WDI\_密码\_算法**](https://msdn.microsoft.com/library/windows/hardware/dn897802)结构。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                            | 描述                            |
|-----------------------------------------------------------------|----------------------------------------|
| [**WDI\_CIPHER\_ALGORITHM**](https://msdn.microsoft.com/library/windows/hardware/dn897802)\[\] | 单播密码算法的数组。 |

 

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

 

 




