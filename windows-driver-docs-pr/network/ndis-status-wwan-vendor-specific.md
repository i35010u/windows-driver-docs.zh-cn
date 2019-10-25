---
title: NDIS_STATUS_WWAN_VENDOR_SPECIFIC
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_VENDOR_SPECIFIC 通知为特定于供应商的操作或供应商特定的更改通知实现事务完成响应。
ms.assetid: 2032ed5e-8a4a-4c1c-9dbe-05e7cec1b683
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_VENDOR_SPECIFIC 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3d7e66cda2941f45fc8aa93298c6e99201510ed6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834650"
---
# <a name="ndis_status_wwan_vendor_specific"></a>\_WWAN\_供应商\_特定的 NDIS\_状态


小型端口驱动程序使用 NDIS\_状态\_WWAN\_供应商\_特定通知来实现特定于供应商的操作或供应商特定更改通知的事务完成响应。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_供应商\_特定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_vendor_specific)的结构。

<a name="remarks"></a>备注
-------

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
<td><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_供应商\_特定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_vendor_specific)

[OID\_WWAN\_供应商\_特定](oid-wwan-vendor-specific.md)

 

 




