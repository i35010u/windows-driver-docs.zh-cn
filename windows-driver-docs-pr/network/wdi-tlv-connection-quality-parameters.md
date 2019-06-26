---
title: WDI_TLV_CONNECTION_QUALITY_PARAMETERS
description: WDI_TLV_CONNECTION_QUALITY_PARAMETERS 是包含所需的 Wi-fi 连接质量提示 TLV。
ms.assetid: A371FD3A-5BF9-4921-AB8E-1651789FA9A1
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CONNECTION_QUALITY_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5e519a5a255d37f3cb4f72ea0f8ef82523b404b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358578"
---
# <a name="wditlvconnectionqualityparameters"></a>WDI\_TLV\_连接\_质量\_参数


WDI\_TLV\_连接\_质量\_参数是包含所需的 Wi-fi 连接质量提示 TLV。

## <a name="tlv-type"></a>TLV 类型


0xA3

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                          |
|--------|--------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 所需的 Wi-fi 连接质量提示中, 定义[ **WDI\_连接\_质量\_提示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_connection_quality_hint)。 |

 

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

 

 




