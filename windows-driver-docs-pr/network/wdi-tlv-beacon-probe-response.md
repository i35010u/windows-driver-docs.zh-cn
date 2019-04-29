---
title: WDI_TLV_BEACON_PROBE_RESPONSE
description: WDI_TLV_BEACON_PROBE_RESPONSE 是包含最新信息或接收端口的探测响应帧 TLV。
ms.assetid: D1148F9B-D25F-4AF0-8C55-43453441C667
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BEACON_PROBE_RESPONSE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6b1d741c6833a2f8453fac159bd6c952fcee80e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361987"
---
# <a name="wditlvbeaconproberesponse"></a>WDI\_TLV\_信号\_探测\_响应


WDI\_TLV\_信号\_探测\_响应是包含最新信息或接收端口的探测响应帧 TLV。

## <a name="tlv-type"></a>TLV 类型


0x30

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 指定的最新信息或由端口收到探测响应框架 UINT8 元素的数组。 这不包括 802.11 MAC 报头。 |

 

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

 

 




