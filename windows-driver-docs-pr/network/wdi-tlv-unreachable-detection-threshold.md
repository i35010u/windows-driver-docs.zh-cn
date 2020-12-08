---
title: WDI_TLV_UNREACHABLE_DETECTION_THRESHOLD
description: WDI_TLV_UNREACHABLE_DETECTION_THRESHOLD 为 TLV，其中包含无法访问的检测阈值。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_UNREACHABLE_DETECTION_THRESHOLD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 462986ceccddc108e2777a843e024d348fa2a85f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834127"
---
# <a name="wdi_tlv_unreachable_detection_threshold"></a>WDI \_ TLV \_ 无法访问 \_ 检测 \_ 阈值


WDI \_ tlv \_ 无法访问 \_ 检测 \_ 阈值是包含无法访问的检测阈值的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xB1

## <a name="length"></a>长度


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 描述                                                                                                                                                                                                                                                                                                               |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 无法访问的检测阈值。 指定802.11 工作站确定其失去了对等设备的连接之前的最大时间量（以毫秒为单位）。 工作站必须在进行此连接性损失确定时包括丢失的信标，但也可以使用它所需的任何其他试探法。 |

 

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

 

 




