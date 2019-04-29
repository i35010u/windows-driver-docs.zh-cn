---
title: WDI_TLV_ADDITIONAL_IES
description: WDI_TLV_ADDITIONAL_IES 是包含其他信息元素 (IE) 设置 TLV。
ms.assetid: B9094E9D-894F-4B23-B4DA-126F87E908C9
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ADDITIONAL_IES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b9435f3958ae96bf91457b629d5ab9e80c9e5e21
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380561"
---
# <a name="wditlvadditionalies"></a>WDI\_TLV\_ADDITIONAL\_IES


WDI\_TLV\_其他\_导致浏览器是包含其他信息元素 (IE) 设置 TLV。

## <a name="tlv-type"></a>TLV 类型


0x8A

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                                       | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                                                                                                                                                          |
|------------------------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_ADDITIONAL\_BEACON\_IES**](wdi-tlv-additional-beacon-ies.md)                                 |                                | X        | 信号而导致浏览器的数组。 Wi-Fi Direct 端口必须将这些附加导致浏览器添加到信号数据包时充当组所有者。 Wi-Fi Direct 端口在设备或客户端模式下操作时，这将忽略。                                                                                              |
| [**WDI\_TLV\_其他\_探测\_响应\_导致浏览器**](wdi-tlv-additional-probe-response-ies.md)                |                                | X        | 探测响应导致浏览器的数组。 Wi-Fi Direct 端口必须将这些附加导致浏览器添加到探测响应数据包时充当 Wi-Fi Direct 设备或组的所有者。 在客户端模式下运行的 Wi-Fi Direct 端口时，这将忽略。                                                                 |
| [**WDI\_TLV\_ADDITIONAL\_PROBE\_REQUEST\_DEFAULT\_IES**](wdi-tlv-additional-probe-request-default-ies.md) |                                | X        | 附加的探测请求导致浏览器的数组。 此偏移量是缓冲区的相对于包含此结构开始。 Wi-Fi Direct 端口必须将这些附加导致浏览器添加到传输的探测请求数据包。 请注意，Wi-Fi Direct 发现请求可能会重写默认的探测请求导致浏览器。 |

 

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

 

 




