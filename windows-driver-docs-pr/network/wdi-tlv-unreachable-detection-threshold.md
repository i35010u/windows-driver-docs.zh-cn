---
title: WDI_TLV_UNREACHABLE_DETECTION_THRESHOLD
description: WDI_TLV_UNREACHABLE_DETECTION_THRESHOLD 是包含无法访问检测阈值 TLV。
ms.assetid: D2C41B26-90EF-4A62-A105-DBEF3822BA6E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_UNREACHABLE_DETECTION_THRESHOLD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a557610cb4e19049936195e4dbe031b3e792d10b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344211"
---
# <a name="wditlvunreachabledetectionthreshold"></a>WDI\_TLV\_无法到达\_检测\_阈值


WDI\_TLV\_无法到达\_检测\_阈值是包含无法访问检测阈值 TLV。

## <a name="tlv-type"></a>TLV 类型


0xB1

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                                                                                                                                                                                               |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 无法访问检测阈值。 802.11 工作站确定它具有到对等设备断开连接之前，请指定最长时间，以毫秒为单位。 工作站必须包括丢失的信标中进行此连接丢失决定，但也可以使用它所需要的任何其他试探方法。 |

 

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

 

 




