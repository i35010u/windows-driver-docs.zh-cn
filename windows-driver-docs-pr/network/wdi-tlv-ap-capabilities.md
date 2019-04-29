---
title: WDI_TLV_AP_CAPABILITIES
description: WDI_TLV_AP_CAPABILITIES 是 TLV，其中包含访问点的功能。
ms.assetid: 2DE866C8-9414-46D8-A156-3A35F1E325EF
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_AP_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7b3d2f981feba63dd6f43a012e9719e16920bc0c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362845"
---
# <a name="wditlvapcapabilities"></a>WDI\_TLV\_AP\_功能


WDI\_TLV\_AP\_功能是包含的功能的访问点 TLV。

## <a name="tlv-type"></a>TLV 类型


0x16

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>扫描 SSID 列表的大小。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>所需的 SSID 列表大小。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>隐私例外列表的大小。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>关联表的大小。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>密钥映射表的大小。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>默认表大小。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>WEP 密钥值的最大长度。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定是否 AP 支持雷达图检测。
<p>有效值为 0 （不支持） 和 1 （支持）。</p></td>
</tr>
</tbody>
</table>

 

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

 

 




