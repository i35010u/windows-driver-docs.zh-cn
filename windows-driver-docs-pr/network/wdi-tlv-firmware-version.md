---
title: WDI_TLV_FIRMWARE_VERSION
description: WDI_TLV_FIRMWARE_VERSION 是包含固件版本的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_FIRMWARE_VERSION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a1e9f84138ffc982bd274420d0dfd7cecbd6e324
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837887"
---
# <a name="wdi_tlv_firmware_version"></a>WDI \_ TLV \_ 固件 \_ 版本


WDI \_ tlv \_ 固件 \_ 版本是包含固件版本的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xF4

## <a name="length"></a>长度


Char 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型     | 描述                                                     |
|----------|-----------------------------------------------------------------|
| char\[\] | 固件版本，存储为以 null 结尾的 ASCII 字符串。 |

 

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

 

 




