---
title: NDIS_STATUS_WWAN_SYS_CAPS_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SYS_CAPS_INFO 通知来告知 MB 服务关于完成的上一个 OID_WWAN_SYS_CAPS_INFO 查询请求。
ms.assetid: 653A35EC-29BB-458D-B33C-41EF6EF47A6E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_SYS_CAPS_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: df408cd78839bce928418021e44855ec5c3a6103
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372515"
---
# <a name="ndisstatuswwansyscapsinfo"></a>NDIS\_状态\_WWAN\_SYS\_CAPS\_信息


微型端口驱动程序使用**NDIS\_状态\_WWAN\_SYS\_CAPS\_信息**通知来通知关于完成的上一MB服务[OID\_WWAN\_SYS\_CAP\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sys-caps)查询请求。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

使用此通知[ **NDIS\_WWAN\_SYS\_CAPS\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)结构。

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
<td><p>Windows 10，版本 1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WWAN\_SYS\_CAPS\_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sys-caps)

[**NDIS\_WWAN\_SYS\_CAPS\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)

 

 




