---
title: OID_WWAN_VENDOR_SPECIFIC
description: OID_WWAN_VENDOR_SPECIFIC 允许微型端口驱动程序来实现供应商特定的对象。
ms.assetid: 7c1843bc-3d60-437c-a24d-6da82262a468
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_VENDOR_SPECIFIC 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2b3042935a80dbd04e42fdec56145c45a79536c9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366569"
---
# <a name="oidwwanvendorspecific"></a>OID\_WWAN\_VENDOR\_SPECIFIC


OID\_WWAN\_供应商\_特定于允许微型端口驱动程序来实现供应商特定的对象。

不支持查询请求。

微型端口驱动程序必须处理集请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_供应商\_特定**](ndis-status-wwan-vendor-specific.md)状态通知包含供应商定义的结构来实现私有对象时已完成事务。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN 供应商特定操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-vendor-specific-operations)。

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
<td><p>Version</p></td>
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[WWAN 供应商特定的操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-vendor-specific-operations)

[**NDIS\_STATUS\_WWAN\_VENDOR\_SPECIFIC**](ndis-status-wwan-vendor-specific.md)

 

 




