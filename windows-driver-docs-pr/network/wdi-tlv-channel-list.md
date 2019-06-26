---
title: WDI_TLV_CHANNEL_LIST
description: WDI_TLV_CHANNEL_LIST 是包含一个或多个频道号 TLV。
ms.assetid: DBBA28C2-D80F-409B-BEE6-81B6FEDF7484
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CHANNEL_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ef0bb6f30d9753ee2d3d17ec8dc7f35675301eb3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387204"
---
# <a name="wditlvchannellist"></a>WDI\_TLV\_通道\_列表


WDI\_TLV\_通道\_列表是包含一个或多个频道号 TLV。

## <a name="tlv-type"></a>TLV 类型


0x4

## <a name="length"></a>长度


数组的大小 （以字节为单位） [ **WDI\_通道\_映射\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ns-wditypes-_wdi_channel_mapping_entry)结构。 该数组必须包含一个或多个结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                       | 描述                          |
|----------------------------------------------------------------------------|--------------------------------------|
| [**WDI\_通道\_映射\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ns-wditypes-_wdi_channel_mapping_entry)\[\] | 通道映射项的数组。 |

 

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

 

 




