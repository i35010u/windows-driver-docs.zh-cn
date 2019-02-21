---
title: WDI_TLV_ADAPTER_RESUME_REQUIRED
description: WDI_TLV_ADAPTER_RESUME_REQUIRED 是指定适配器恢复是否需要 TLV。
ms.assetid: 341B871A-F789-447E-A74C-3274B6B8B14A
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ADAPTER_RESUME_REQUIRED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b2f8d2cb5ca268dcc02732dc7913dea6bc9b16bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526403"
---
# <a name="wditlvadapterresumerequired"></a>WDI\_TLV\_适配器\_恢复\_必需


WDI\_TLV\_适配器\_恢复\_必需是指定适配器恢复是否需要 TLV。

## <a name="tlv-type"></a>TLV 类型


0xB7

## <a name="length"></a>长度


超出 UINT8 的大小 （以字节为单位）。

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
<td>指定如果适配器恢复要求。
<p>有效值为 0 （不要求） 和 1 （必需）。 如果设置为 1，固件要求 OS 协助，若要恢复其上下文。</p></td>
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

 

 




