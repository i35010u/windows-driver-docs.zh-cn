---
title: WDI_TLV_COMMUNICATION_CONFIGURATION_ATTRIBUTES
description: WDI_TLV_COMMUNICATION_CONFIGURATION_ATTRIBUTES 是 TLV，其中包含主机适配器通信协议配置特性。
ms.assetid: A779FA2D-D3E0-4FC9-9A8A-09B6E3CFF758
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_COMMUNICATION_CONFIGURATION_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5d89bd797aefc00967f7794350c31ec41620d046
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331222"
---
# <a name="wditlvcommunicationconfigurationattributes"></a>WDI\_TLV\_通信\_配置\_属性


WDI\_TLV\_通信\_配置\_属性是包含的主机适配器通信协议配置特性 TLV。

## <a name="tlv-type"></a>TLV 类型


0x20

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                | 允许多个 TLV 实例 | 可选 | 描述                     |
|-------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------|
| [**WDI\_TLV\_通信\_功能**](wdi-tlv-communication-capabilities.md) |                                | X        | 通信功能中。 |

 

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

 

 




