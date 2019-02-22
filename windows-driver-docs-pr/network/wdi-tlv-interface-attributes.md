---
title: WDI_TLV_INTERFACE_ATTRIBUTES
description: WDI_TLV_INTERFACE_ATTRIBUTES 是接口的 TLV 包含属性。
ms.assetid: A36AC0A7-6F5B-4461-841D-3B4C19BD49EB
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INTERFACE_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 553ea43355a1cec591f6a83d780b97369c93ca23
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544573"
---
# <a name="wditlvinterfaceattributes"></a>WDI\_TLV\_接口\_属性


WDI\_TLV\_接口\_属性是包含属性的接口 TLV。

## <a name="tlv-type"></a>TLV 类型


0x21

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                         | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                                     |
|------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_INTERFACE\_CAPABILITIES**](wdi-tlv-interface-capabilities.md)  |                                |          | 接口的功能。                                                                                                                                                              |
| [**WDI\_TLV\_FIRMWARE\_VERSION**](wdi-tlv-firmware-version.md)              |                                |          | 指定的固件版本为 ASCII 字符串。                                                                                                                                            |
| [**WDI\_TLV\_IHV\_NON\_WDI\_OIDS\_LIST**](wdi-tlv-ihv-non-wdi-oids-list.md) |                                | X        | 列表的非-WDI Oid 适配器要播发到操作系统。 适配器不应假定操作系统已筛选非-WDI Oid 以匹配此列表。 |

 

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
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




