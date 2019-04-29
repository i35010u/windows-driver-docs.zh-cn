---
title: WDI_TLV_ADDITIONAL_PROBE_RESPONSE_IES
description: WDI_TLV_ADDITIONAL_PROBE_RESPONSE_IES 是包含探测响应 IEs TLV。
ms.assetid: BDEDAD4D-A35B-4AE9-BC90-184CD75002B2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ADDITIONAL_PROBE_RESPONSE_IES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0957337ce6c66e8cd9ab1bd86bc5329ff31b46d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382180"
---
# <a name="wditlvadditionalproberesponseies"></a>WDI\_TLV\_其他\_探测\_响应\_导致浏览器


WDI\_TLV\_其他\_探测\_响应\_导致浏览器是包含探测响应 IEs TLV。

## <a name="tlv-type"></a>TLV 类型


0x93

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                                                                                                                                                                                                  |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 探测响应导致浏览器的数组。 Wi-Fi Direct 端口必须将这些附加导致浏览器添加到探测响应数据包时充当 Wi-Fi Direct 设备或组的所有者。 在客户端模式下运行的 Wi-Fi Direct 端口时，将忽略此成员。 |

 

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

 

 




