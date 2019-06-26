---
title: WDI_TLV_ADAPTER_NLO_SCAN_MODE
description: WDI_TLV_ADAPTER_NLO_SCAN_MODE 是 TLV，该值指示是否应在主动或被动模式下执行扫描。
ms.assetid: 4294AF4D-587E-4978-9C54-E11D7368FBB8
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ADAPTER_NLO_SCAN_MODE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1053924c720ee8f2cef3acec977e5660aa7f72c9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381125"
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
| UINT32 | [**WDI\_扫描\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_scan_type)值，该值指示是否应在主动或被动模式下执行扫描。 |

 

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

 

 




