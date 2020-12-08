---
title: WDI_TLV_ADDITIONAL_IES
description: WDI_TLV_ADDITIONAL_IES 是一种 TLV，其中包含 (IE) 设置的附加信息元素。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ADDITIONAL_IES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cf96c92d32c1aad226ca6b4211cc7d735aded18b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822035"
---
# <a name="wdi_tlv_additional_ies"></a>WDI \_ TLV \_ 补充 \_


WDI \_ tlv \_ 附加的 \_ tlv 是包含其他 Information (元素的 tlv) 设置。

## <a name="tlv-type"></a>TLV 类型


0x8A

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                                       | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                                                                                                                                                                          |
|------------------------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 附加的 \_ 信标 \_**](wdi-tlv-additional-beacon-ies.md)                                 |                                | X        | 一组信号。 Wi-Fi 直接端口在作为组所有者时，必须将这些附加的添加到信号数据包中。 当 Wi-Fi 直接端口在设备或客户端模式下操作时，将忽略此项。                                                                                              |
| [**WDI \_ TLV \_ 附加的 \_ 探测 \_ 响应 \_**](wdi-tlv-additional-probe-response-ies.md)                |                                | X        | 发出的探测响应的数组。 Wi-Fi 直接端口在 Wi-Fi 充当直接设备或组所有者时，必须将这些附加包添加到探测响应数据包中。 当 Wi-Fi 直接端口在客户端模式下操作时，将忽略此项。                                                                 |
| [**WDI \_ TLV \_ 附加 \_ 探测 \_ 请求 \_ 默认值 \_**](wdi-tlv-additional-probe-request-default-ies.md) |                                | X        | 发出附加探测请求的数组。 此偏移量相对于包含此结构的缓冲区的开头。 Wi-Fi 直接端口必须将这些附加的附加到它传输的探测请求数据包中。 请注意，Wi-Fi 的直接发现请求可能会覆盖默认的探测请求。 |

 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




