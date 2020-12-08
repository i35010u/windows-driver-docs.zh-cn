---
title: WDI_TLV_COMMUNICATION_CONFIGURATION_ATTRIBUTES
description: WDI_TLV_COMMUNICATION_CONFIGURATION_ATTRIBUTES 是包含主机适配器通信协议配置特性的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_COMMUNICATION_CONFIGURATION_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ca0f8014cdaf32e33eba27b00c96b89cd9948732
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822763"
---
# <a name="wdi_tlv_communication_configuration_attributes"></a>WDI \_ TLV \_ 通信 \_ 配置 \_ 属性


WDI \_ tlv \_ 通信 \_ 配置 \_ 属性是一个 tlv，其中包含主机适配器通信协议配置特性。

## <a name="tlv-type"></a>TLV 类型


0x20

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                | 允许多个 TLV 实例 | 可选 | 说明                     |
|-------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------|
| [**WDI \_ TLV \_ 通信 \_ 功能**](wdi-tlv-communication-capabilities.md) |                                | X        | 通信功能。 |

 

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

 

 




