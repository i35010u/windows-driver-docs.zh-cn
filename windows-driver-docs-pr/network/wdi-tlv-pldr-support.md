---
title: WDI_TLV_PLDR_SUPPORT
description: WDI_TLV_PLDR_SUPPORT 是一种 TLV，用于指定是否支持 PLDR (平台级别重置) 。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PLDR_SUPPORT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 05459f939a150b88ba171c075767c856f1edc490
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818069"
---
# <a name="wdi_tlv_pldr_support"></a>WDI \_ TLV \_ PLDR \_ 支持


WDI \_ tlv \_ PLDR \_ 支持是一个 tlv，用于指定是否支持 PLDR (平台级别重置) 。

**注意**  此 TLV 已添加到 Windows 10 版本1511，WDI 版本1.0.10 中。

 

## <a name="tlv-type"></a>TLV 类型


0x11A

## <a name="length"></a>长度


UINT8 的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型  | 描述                                                                                                                                                                                                                       |
|-------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | 指定是否支持 PLDR。 如果设备或总线不支持重置功能，则此值设置为0， (通常通过查询 ACPI 或 PCI 方法) 。 非零值指定支持重置功能。 |

 

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

## <a name="see-also"></a>请参阅


[PLDR](./wdi-pldr-and-fldr.md)

 

