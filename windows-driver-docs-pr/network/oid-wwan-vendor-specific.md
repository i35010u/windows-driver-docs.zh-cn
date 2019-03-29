---
title: OID_WWAN_VENDOR_SPECIFIC
description: OID_WWAN_VENDOR_SPECIFIC 允许微型端口驱动程序来实现供应商特定的对象。
ms.assetid: 7c1843bc-3d60-437c-a24d-6da82262a468
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_VENDOR_SPECIFIC 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4a647fe74b14f5ca8c7ddaed8156046c0c7d4d31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568611"
---
# <a name="oidwwanvendorspecific"></a>OID\_WWAN\_VENDOR\_SPECIFIC


OID\_WWAN\_供应商\_特定于允许微型端口驱动程序来实现供应商特定的对象。

不支持查询请求。

微型端口驱动程序必须处理集请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_供应商\_特定**](ndis-status-wwan-vendor-specific.md)状态通知包含供应商定义的结构来实现私有对象时已完成事务。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN 供应商特定操作](https://msdn.microsoft.com/library/windows/hardware/ff559138)。

微型端口驱动程序应返回 NDIS\_状态\_不\_支持如果它们不支持特定于供应商的操作。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[WWAN 供应商特定的操作](https://msdn.microsoft.com/library/windows/hardware/ff559138)

[**NDIS\_STATUS\_WWAN\_VENDOR\_SPECIFIC**](ndis-status-wwan-vendor-specific.md)

 

 




