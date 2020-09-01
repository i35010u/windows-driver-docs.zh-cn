---
title: NDIS_STATUS_WWAN_IP_ADDRESS_STATE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_IP_ADDRESS_STATE 通知来通知 MB 服务有关 IP 配置的更改的额外 PDP 上下文。
ms.assetid: 98E4028D-AD75-4F12-ADA4-41725253166F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_IP_ADDRESS_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 568fe0275517f5e1eae56325b0d630fe1ace0a4f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212845"
---
# <a name="ndis_status_wwan_ip_address_state"></a>NDIS \_ 状态 \_ WWAN \_ IP \_ 地址 \_ 状态


微型端口驱动程序使用 NDIS \_ 状态 \_ WWAN \_ IP \_ 地址 \_ 状态通知来通知 MB 服务有关 IP 配置的更改的额外 PDP 上下文。

此通知使用 [**NDIS \_ WWAN \_ IP \_ 地址 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ip_address_state) 结构。

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
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ WWAN \_ IP \_ 地址 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ip_address_state)

 

