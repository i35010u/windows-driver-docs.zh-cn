---
title: WDI_TLV_CIPHER_KEY_TYPE_INFO
description: WDI_TLV_CIPHER_KEY_TYPE_INFO 是包含密码 OID_WDI_SET_ADD_CIPHER_KEYS 和 OID_WDI_SET_DELETE_CIPHER_KEYS 的密钥类型信息 TLV。
ms.assetid: 1168D53D-A837-4E3F-8E31-FB86CF866BA3
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_TYPE_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6ed6349b7e68d5872ef1b03bdeaf692cfe2ca33c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331828"
---
# <a name="wditlvcipherkeytypeinfo"></a>WDI\_TLV\_CIPHER\_KEY\_TYPE\_INFO


WDI\_TLV\_密码\_密钥\_类型\_信息是包含密码的密钥类型信息 TLV [OID\_WDI\_设置\_添加\_密码\_密钥](https://msdn.microsoft.com/library/windows/hardware/dn925855)并[OID\_WDI\_设置\_删除\_密码\_密钥](https://msdn.microsoft.com/library/windows/hardware/dn925929)。

## <a name="tlv-type"></a>TLV 类型


0x4E

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                 | 描述                                                                                                                                                                                                                                                                                     |
|----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_密码\_算法**](https://msdn.microsoft.com/library/windows/hardware/dn897802)          | 指定将使用的密钥的密码算法。                                                                                                                                                                                                                                               |
| [**WDI\_CIPHER\_KEY\_DIRECTION**](https://msdn.microsoft.com/library/windows/hardware/dn897803) | 指定是否应为使用该密钥仅传输，仅，接收和 / 或。                                                                                                                                                                                                              |
| UINT8                                                                | 指定该端口是否应删除上漫游的项。 如果此值设置为 0，端口从 BSS 网络断开连接或连接到的 BSS 网络时，必须删除该密钥。 如果此值设置为 1，在显式删除或重置请求，应删除的密钥。 |
| [**WDI\_CIPHER\_KEY\_TYPE**](https://msdn.microsoft.com/library/windows/hardware/dn897806)           | 指定要发布的键的类型。                                                                                                                                                                                                                                                      |

 

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

 

 




