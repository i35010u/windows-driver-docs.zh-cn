---
title: WDI_TLV_CONNECTION_QUALITY_PARAMETERS
description: WDI_TLV_CONNECTION_QUALITY_PARAMETERS 是一个 TLV，其中包含所需的 Wi-fi 连接质量提示。
ms.assetid: A371FD3A-5BF9-4921-AB8E-1651789FA9A1
ms.date: 07/18/2017
keywords:
- WDI_TLV_CONNECTION_QUALITY_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 323d5633202b7394c9150c71c43c9c736a4617c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843388"
---
# <a name="wdi_tlv_connection_quality_parameters"></a>WDI\_TLV\_连接\_质量\_参数


WDI\_TLV\_连接\_质量\_参数是包含所需 Wi-fi 连接质量提示的 TLV。

## <a name="tlv-type"></a>TLV 类型


0xA3

## <a name="length"></a>长度


UINT32 的大小（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                          |
|--------|--------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | [**WDI\_连接\_Quality\_提示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_connection_quality_hint)中定义的所需 Wi-fi 连接质量提示。 |

 

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
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




