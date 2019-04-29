---
title: WDI_TLV_ADDITIONAL_BEACON_IES
description: WDI_TLV_ADDITIONAL_BEACON_IES 是包含其他信号 IEs TLV。
ms.assetid: 7B4D863A-1480-4283-A5E9-5F4F043B0CDE
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ADDITIONAL_BEACON_IES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 63f36e5cc676fd3a165a5efeb4c78868c1741db4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380563"
---
# <a name="wditlvadditionalbeaconies"></a>WDI\_TLV\_其他\_信号\_导致浏览器


WDI\_TLV\_其他\_发信号的\_导致浏览器是包含其他信号 IEs TLV。

## <a name="tlv-type"></a>TLV 类型


0x98

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                                                                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 信号而导致浏览器的数组。 Wi-Fi Direct 端口必须将这些附加导致浏览器添加到信号数据包时充当组所有者。 Wi-Fi Direct 端口在设备或客户端模式下操作时，将忽略这些。 |

 

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

 

 




