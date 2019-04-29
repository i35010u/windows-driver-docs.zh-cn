---
title: WDI_TLV_RECEIVE_COALESCE_OFFLOAD_CAPABILITIES
description: WDI_TLV_RECEIVE_COALESCE_OFFLOAD_CAPABILITIES 是包含 Rx TLV coalesce 卸载功能。
ms.assetid: AF13B304-3E94-42EE-8BBB-107F5F238758
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_RECEIVE_COALESCE_OFFLOAD_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7c58c4a917784767462bf5c60d7dc960463532fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359724"
---
# <a name="wditlvreceivecoalesceoffloadcapabilities"></a>WDI\_TLV\_接收\_COALESCE\_卸载\_功能


WDI\_TLV\_接收\_COALESCE\_卸载\_功能是包含 Rx TLV coalesce 卸载功能。

## <a name="tlv-type"></a>TLV 类型


0xCE

## <a name="length"></a>长度


大小 （以字节为单位） 的以下值。

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
<td>指定是否 Rx coalesce IPv4 为启用。
<p>有效值为 0 （未启用） 和 1 （启用）。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定是否 Rx coalesce 对 IPv6 的启用。
<p>有效值为 0 （未启用） 和 1 （启用）。</p></td>
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

 

 




