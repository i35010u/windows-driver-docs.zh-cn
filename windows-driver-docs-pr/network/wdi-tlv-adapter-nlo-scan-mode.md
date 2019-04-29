---
title: WDI_TLV_ADAPTER_NLO_SCAN_MODE
description: WDI_TLV_ADAPTER_NLO_SCAN_MODE 是 TLV，该值指示是否应在主动或被动模式下执行扫描。
ms.assetid: 4294AF4D-587E-4978-9C54-E11D7368FBB8
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ADAPTER_NLO_SCAN_MODE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 95dadeb161840e0e4d975d40c701159b3fa5147d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356817"
---
# <a name="wditlvadapternloscanmode"></a>WDI\_TLV\_适配器\_NLO\_扫描\_模式


WDI\_TLV\_适配器\_NLO\_扫描\_模式是 TLV，该值指示是否应在主动或被动模式下执行扫描。

## <a name="tlv-type"></a>TLV 类型


0x125

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                     |
|--------|---------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | [**WDI\_扫描\_类型**](https://msdn.microsoft.com/library/windows/hardware/dn926115)值，该值指示是否应在主动或被动模式下执行扫描。 |

 

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

 

 




