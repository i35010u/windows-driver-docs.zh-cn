---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_REMOVE
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_REMOVE 是包含协议 TLV 卸载与 OID_WDI_SET_REMOVE_PM_PROTOCOL_OFFLOAD 移除 ID。
ms.assetid: BD74C9F7-6370-41D5-841F-6949D7748E30
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PM_PROTOCOL_OFFLOAD_REMOVE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 779f047d2fef0119316cd945bfafbff74de34792
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523549"
---
# <a name="wditlvpmprotocoloffloadremove"></a>WDI\_TLV\_PM\_PROTOCOL\_OFFLOAD\_REMOVE


WDI\_TLV\_PM\_协议\_卸载\_删除是包含要删除的协议卸载 ID TLV [OID\_WDI\_集\_删除\_PM\_协议\_卸载](https://msdn.microsoft.com/library/windows/hardware/dn925943)。

## <a name="tlv-type"></a>TLV 类型


0x6C

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                        |
|--------|------------------------------------|
| UINT32 | 指定协议卸载 id。 |

 

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

 

 




