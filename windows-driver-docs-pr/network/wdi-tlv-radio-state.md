---
title: WDI_TLV_RADIO_STATE
description: WDI_TLV_RADIO_STATE 是包含在硬件和软件无线电状态 TLV。
ms.assetid: 0DAE1D0A-4EEC-4054-A67C-EC3B5EDF77A5
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_RADIO_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0907fb119a7f48afbad2d66f0ec15b6d5e88d762
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554025"
---
# <a name="wditlvradiostate"></a>WDI\_TLV\_RADIO\_STATE


WDI\_TLV\_单选\_状态是包含在硬件和软件无线电状态 TLV。

## <a name="tlv-type"></a>TLV 类型


0xA1

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
<td>UINT8</td>
<td>在硬件中的单选当前状态。
<p>有效值为 0 和 1。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>在软件中的单选当前状态。
<p>有效值为 0 和 1。</p></td>
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
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




