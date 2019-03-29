---
title: WDI_TLV_POWER_STATE
description: WDI_TLV_POWER_STATE 是包含电源状态 TLV。
ms.assetid: EC65FE08-ABF0-488A-A6FA-21B1794418B3
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_POWER_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1f1b24240693da7075c8a90ebc5dc4986e79cfe4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565753"
---
# <a name="wditlvpowerstate"></a>WDI\_TLV\_POWER\_STATE


WDI\_TLV\_电源\_状态是包含电源状态 TLV。

## <a name="tlv-type"></a>TLV 类型


0x44

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

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
<td>指定的电源状态。
<p>有效值包括：</p>
<ul>
<li>0x0001:退出低能耗 (D0)</li>
<li>0x0003:输入低能耗 (D2)</li>
<li>0x0004:输入关闭电源 （D3，可能不实际进行电源已关闭在某些平台上）</li>
</ul></td>
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

 

 




