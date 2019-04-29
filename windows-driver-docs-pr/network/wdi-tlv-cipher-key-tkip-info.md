---
title: WDI_TLV_CIPHER_KEY_TKIP_INFO
description: WDI_TLV_CIPHER_KEY_TKIP_INFO 是包含 TKIP 信息 TLV。
ms.assetid: 330A93F5-43E7-4A4A-A6BD-EF276D6F09A1
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_TKIP_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 610bf9bdaa365c5826b5ae869740204978aa2819
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391006"
---
# <a name="wditlvcipherkeytkipinfo"></a>WDI\_TLV\_密码\_密钥\_TKIP\_信息


WDI\_TLV\_密码\_密钥\_TKIP\_信息是包含 TKIP 信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0x4B

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                    | 允许多个 TLV 实例 | 可选 | 描述                      |
|-------------------------------------------------------------------------|--------------------------------|----------|----------------------------------|
| [**WDI\_TLV\_CIPHER\_KEY\_TKIP\_KEY**](wdi-tlv-cipher-key-tkip-key.md) |                                |          | 指定 TKIP 密钥材料。 |
| [**WDI\_TLV\_CIPHER\_KEY\_TKIP\_MIC**](wdi-tlv-cipher-key-tkip-mic.md) |                                |          | 指定 TKIP MIC 材料。 |

 

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

 

 




