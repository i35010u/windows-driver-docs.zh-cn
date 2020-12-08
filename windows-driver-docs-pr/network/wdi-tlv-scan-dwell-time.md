---
title: WDI_TLV_SCAN_DWELL_TIME
description: WDI_TLV_SCAN_DWELL_TIME 是包含扫描停留时间设置的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SCAN_DWELL_TIME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1270a408d1972e4dd2368c1bdc3562e907007e18
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834179"
---
# <a name="wdi_tlv_scan_dwell_time"></a>WDI \_ TLV \_ 扫描 \_ 停留 \_ 时间


WDI \_ tlv \_ 扫描 \_ 停留 \_ 时间是包含扫描停留时间设置的 TLV。

## <a name="tlv-type"></a>TLV 类型


0x7

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型   | 描述                                                                                                                                                                           |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 指定停留在活动频道上的时间（以毫秒为单位）。 这是一个提示，如果适配器决定使用其自己的停留时间，则必须满足最长扫描时间要求。  |
| UINT32 | 指定在被动通道上停留的时间（以毫秒为单位）。 这是一个提示，如果适配器决定使用其自己的停留时间，则必须满足最长扫描时间要求。 |
| UINT32 | 指定扫描总计的时间（以毫秒为单位）。 如果适配器将其停留时间限制在上面指定的值以下，则它可以忽略最大扫描时间参数。          |

 

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

 

 




