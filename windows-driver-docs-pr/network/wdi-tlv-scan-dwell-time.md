---
title: WDI_TLV_SCAN_DWELL_TIME
description: WDI_TLV_SCAN_DWELL_TIME 是 TLV 包含扫描停留时间设置。
ms.assetid: A0C597E7-879C-43CC-BB86-4908AC31828F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SCAN_DWELL_TIME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2bf470aba7780223e2d2d609b255198663a392ad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330719"
---
# <a name="wditlvscandwelltime"></a>WDI\_TLV\_SCAN\_DWELL\_TIME


WDI\_TLV\_扫描\_会仔细斟酌\_时间是 TLV 包含扫描停留时间设置。

## <a name="tlv-type"></a>TLV 类型


0x7

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                                                           |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 指定的时间以毫秒为单位来活动通道在此再次详述。 这是一个提示，并且如果适配器决定使用自己的停留时间，它必须满足的最长扫描时间要求。  |
| UINT32 | 指定以毫秒为单位来会仔细斟酌在被动的通道上的时间。 这是一个提示，并且如果适配器决定使用自己的停留时间，它必须满足的最长扫描时间要求。 |
| UINT32 | 以毫秒为单位的总扫描指定的时间。 如果适配器限制到其停留时间低于以上指定的值，它可以忽略的最长扫描时间参数。          |

 

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

 

 




