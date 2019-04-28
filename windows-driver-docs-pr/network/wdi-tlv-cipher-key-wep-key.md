---
title: WDI_TLV_CIPHER_KEY_WEP_KEY
description: WDI_TLV_CIPHER_KEY_WEP_KEY 是包含 WEP 密钥 TLV。
ms.assetid: 22C332B4-A9A7-4205-9ADA-80914FB34642
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_WEP_KEY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8386be57ea8bcab866c4dc680be977d95e73e3ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331822"
---
# <a name="wditlvcipherkeywepkey"></a>WDI\_TLV\_CIPHER\_KEY\_WEP\_KEY


WDI\_TLV\_密码\_密钥\_WEP\_键是包含 WEP 密钥 TLV。

## <a name="tlv-type"></a>TLV 类型


0x58

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                            |
|-----------|--------------------------------------------------------|
| UINT8\[\] | 指定的 WEP 密钥 UINT8 元素的数组。 |

 

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

 

 




