---
title: OID_PD_CLOSE_PROVIDER
description: NDIS 协议或筛选器驱动程序将对象标识符 (OID) 方法 OID_PD_CLOSE_PROVIDER 请求发送到 PDPI 提供程序，以在 PDPI 提供程序对象中提供对 PD 功能的访问权限。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PD_CLOSE_PROVIDER 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f1680b9bbe106a1a5965682e583e7f7b0228f345
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822129"
---
# <a name="oid_pd_close_provider"></a>OID \_ PD \_ 关闭 \_ 提供程序


NDIS 协议或筛选器驱动程序向 PDPI 提供程序发送对象标识符 (OID) 方法请求，以便在 \_ \_ \_ PDPI 提供程序对象中对 PD 功能进行访问。

当 NDIS 协议或筛选器驱动程序收到取消绑定通知、暂停指示、低能耗事件或 PD 配置更改事件（指示在绑定上禁用了 PD）时，它必须调用此 OID。

在调用此 OID 之前，NDIS 协议或筛选器驱动程序必须确保它已关闭并释放了通过 PD 提供程序实例创建的所有 PD 对象，例如队列、计数器和筛选器。 在发出此 OID 之前，NDIS 协议或筛选器驱动程序必须保证不存在对任何 PD 提供程序调度表函数的正在进行的调用。

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)

[**NDIS \_ PD \_ 关闭 \_ 提供程序 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_close_provider_parameters)

[NDIS \_ 状态 \_ PD \_ 当前 \_ 配置](./ndis-status-pd-current-config.md)

[OID \_ PD \_ 打开 \_ 提供程序](oid-pd-open-provider.md)

 

