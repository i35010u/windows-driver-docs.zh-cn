---
title: WDI_TLV_CIPHER_KEY_RECEIVE_SEQUENCE_COUNT
description: WDI_TLV_CIPHER_KEY_RECEIVE_SEQUENCE_COUNT 是包含接收序列计数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_RECEIVE_SEQUENCE_COUNT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3bb613f5bc9ae48572f7a1824f6b5a685f6ffd32
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837641"
---
# <a name="wdi_tlv_cipher_key_receive_sequence_count"></a>WDI \_ TLV \_ 密码 \_ 密钥 \_ 接收 \_ 序列 \_ 计数


WDI \_ tlv \_ 密码 \_ 密钥 \_ 接收 \_ 序列 \_ 计数是包含接收序列计数的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x4F

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型       | 描述                                                                                    |
|------------|------------------------------------------------------------------------------------------------|
| UINT8 \[ 6\] | 指定 (PN) 的数据包编号的初始48位值，用于重放保护。 |

 

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

 

 




