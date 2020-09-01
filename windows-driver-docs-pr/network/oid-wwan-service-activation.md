---
title: OID_WWAN_SERVICE_ACTIVATION
description: OID_WWAN_SERVICE_ACTIVATION 指示微型端口驱动程序启动服务激活，以便获得访问提供商网络的权限。
ms.assetid: a70c087d-0650-4aab-b78e-0d5a7aa49eb6
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SERVICE_ACTIVATION 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: de6b1825701fc4080895679a2deae1e8b304847e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218343"
---
# <a name="oid_wwan_service_activation"></a>OID \_ WWAN \_ 服务 \_ 激活


OID \_ WWAN \_ 服务 \_ 激活指示微型端口驱动程序启动服务激活，以便获得访问提供商网络的权限。

不支持查询请求。

微型端口驱动程序必须异步处理设置请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [**ndis \_ 状态 \_ WWAN \_ 服务 \_ 激活**](ndis-status-wwan-service-activation.md) 状态通知，其中包含 [**ndis \_ WWAN \_ 服务 \_ 激活**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation) 结构，以启动服务激活，以便在客户完成该事务时获得访问提供者网络的访问权限。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅 [MB 服务检测和激活](./mb-service-detection-and-activation.md)。

小型端口驱动程序可以在处理查询或设置请求时 (SIM 卡) 或提供程序网络访问订阅服务器标识模块。

\_ \_ \_ 在服务激活过程需要微型端口驱动程序和用户交互的情况下，MB 服务使用 OID WWAN 服务激活。

这不是启用小型小型驱动程序启动或带外手动服务激活（例如，调用服务提供商的支持人员）所必需的。 在按上述方案激活设备后，如果当前微型端口驱动程序 **ReadyState** 为 *WwanReadyStateNotActivated*，则微型端口驱动程序应继续使用 MB 初始化，并使用 NDIS \_ 状态 \_ WWAN \_ 就绪 \_ 信息指示通知 mb 服务的就绪状态更改。

如果微型端口驱动程序 \_ 不 \_ \_ 支持基于微型端口驱动程序的服务激活，则它应返回不受支持的 NDIS 状态。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID \_ WWAN \_ 就绪 \_ 信息](oid-wwan-ready-info.md)

[**NDIS \_ WWAN \_ 服务 \_ 激活**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation)

[**NDIS \_ 状态 \_ WWAN \_ 服务 \_ 激活**](ndis-status-wwan-service-activation.md)

[MB 服务检测和激活](./mb-service-detection-and-activation.md)

 

