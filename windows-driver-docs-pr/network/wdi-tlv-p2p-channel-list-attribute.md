---
title: WDI_TLV_P2P_CHANNEL_LIST_ATTRIBUTE
description: WDI_TLV_P2P_CHANNEL_LIST_ATTRIBUTE 是 TLV，其中包含通道列表特性。
ms.assetid: 2378AC49-1530-45E2-A7C8-FEAF5E6CDBE5
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_CHANNEL_LIST_ATTRIBUTE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3a3d1a6570bee286b0b1b915b660e9bdd6712b2c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541994"
---
# <a name="wditlvp2pchannellistattribute"></a>WDI\_TLV\_P2P\_CHANNEL\_LIST\_ATTRIBUTE


WDI\_TLV\_P2P\_通道\_列表\_属性是包含通道列表特性 TLV。

## <a name="tlv-type"></a>TLV 类型


0xD5

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                          | 允许多个 TLV 实例 | 可选 | 描述              |
|-------------------------------------------------------------------------------|--------------------------------|----------|--------------------------|
| [**WDI\_TLV\_国家/地区\_区域\_列表**](wdi-tlv-country-region-list.md)        |                                |          | 国家/地区列表中。 |
| [**WDI\_TLV\_P2P\_通道\_条目\_列表**](wdi-tlv-p2p-channel-entry-list.md) | X                              |          | 频道列表。    |

 

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

 

 




