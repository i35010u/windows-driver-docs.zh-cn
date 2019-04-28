---
title: NDIS_STATUS_WWAN_PIN_LIST
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_PIN_LIST 通知来响应的 OID_WWAN_PIN_LIST OID 查询请求。 微型端口驱动程序不能使用此通知将发送未经请求的事件。此通知使用 NDIS_WWAN_PIN_LIST 结构。
ms.assetid: fd8e6734-d032-445a-819a-0d5a773e9ea3
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_PIN_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cd02f5297bb72fd0d69237a8fd919e2aed511f5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341395"
---
# <a name="ndisstatuswwanpinlist"></a>NDIS\_STATUS\_WWAN\_PIN\_LIST


微型端口驱动程序使用 NDIS\_状态\_WWAN\_PIN\_OID 查询请求的响应的列表通知[OID\_WWAN\_PIN\_列表](oid-wwan-pin-list.md).

微型端口驱动程序不能使用此通知将发送未经请求的事件。

使用此通知[ **NDIS\_WWAN\_PIN\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff567912)结构。

<a name="remarks"></a>备注
-------

这种指示是响应仅通知 OID 查询请求的 OID\_WWAN\_PIN\_列表。 为此可能不应未经请求的指示。

由于 OID 而导致的 PIN 输入模式中的任何更改\_WWAN\_PIN 启用或禁用操作不会导致 NDIS\_状态\_WWAN\_PIN\_列表指示。

请注意，所有设备支持球瓶当前 PinMode 必须都更新以反映当前状态的每个查询请求上的微型端口驱动程序。

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
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WWAN\_PIN\_LIST](oid-wwan-pin-list.md)

[**NDIS\_WWAN\_PIN\_LIST**](https://msdn.microsoft.com/library/windows/hardware/ff567912)

 

 




