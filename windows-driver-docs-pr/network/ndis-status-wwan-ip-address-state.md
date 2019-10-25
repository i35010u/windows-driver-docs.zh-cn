---
title: NDIS_STATUS_WWAN_IP_ADDRESS_STATE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_IP_ADDRESS_STATE 通知来通知 MB 服务有关 IP 配置的更改的额外 PDP 上下文。
ms.assetid: 98E4028D-AD75-4F12-ADA4-41725253166F
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_IP_ADDRESS_STATE 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c547aec60bd2c0334db6d282bc2f66fc3a16095a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843026"
---
# <a name="ndis_status_wwan_ip_address_state"></a>\_WWAN\_IP\_地址\_状态的 NDIS\_状态


小型端口驱动程序使用 NDIS\_状态\_WWAN\_IP\_地址\_状态通知来通知 MB 服务有关 IP 配置的更改的额外 PDP 上下文。

此通知使用[**NDIS\_WWAN\_IP\_地址\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ip_address_state)结构。

<a name="remarks"></a>备注
-------

必须在与其他 PDP 上下文会话关联的 NDIS 端口上发送此通知。

如果已成功激活额外的 PDP 上下文并且已获取该上下文的 IP 配置，微型端口驱动程序应发送此通知。 如果设备指示在上下文激活后发生了未经请求的 IP 配置更改，则微型端口驱动程序应使用更新的 IP 配置发送此通知的未经请求的指示。

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
<td><p>在 Windows 8.1 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_IP\_地址\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ip_address_state)

 

 




