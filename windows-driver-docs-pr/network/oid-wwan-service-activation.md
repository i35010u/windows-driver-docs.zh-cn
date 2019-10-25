---
title: OID_WWAN_SERVICE_ACTIVATION
description: OID_WWAN_SERVICE_ACTIVATION 指示微型端口驱动程序启动服务激活，以便获得访问提供商网络的权限。
ms.assetid: a70c087d-0650-4aab-b78e-0d5a7aa49eb6
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SERVICE_ACTIVATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 97ec330be6aeeee3c0017fbd7d67f495e15ddc6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843794"
---
# <a name="oid_wwan_service_activation"></a>OID\_WWAN\_服务\_激活


OID\_WWAN\_服务\_激活指示微型端口驱动程序启动服务激活，以便获得访问提供商网络的权限。

不支持查询请求。

微型端口驱动程序必须异步处理设置请求，最初返回 NDIS\_状态\_指示\_需要原始请求，稍后将[**ndis\_状态\_WWAN\_服务发送\_** ](ndis-status-wwan-service-activation.md)包含[**NDIS\_WWAN\_\_服务**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation)的激活状态通知，用于启动服务激活，以便在客户完成该事务时获得访问提供者网络的权限。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[MB 服务检测和激活](https://docs.microsoft.com/windows-hardware/drivers/network/mb-service-detection-and-activation)。

当处理查询或设置请求时，微型端口驱动程序可以访问订阅服务器标识模块（SIM 卡）或提供程序网络。

在服务激活过程需要微型端口驱动程序和用户交互的情况下，MB 服务使用 OID\_WWAN\_服务\_激活。

这不是启用小型小型驱动程序启动或带外手动服务激活（例如，调用服务提供商的支持人员）所必需的。 按上述方案激活设备后，如果当前微型端口驱动程序**ReadyState**为*WwanReadyStateNotActivated*，则微型端口驱动程序应继续进行 mb 初始化，并使用NDIS\_状态\_WWAN\_准备就绪\_信息指示。

如果不支持基于微型端口驱动程序的服务激活，微型端口驱动程序应返回 NDIS\_状态\_不\_支持。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WWAN\_就绪\_信息](oid-wwan-ready-info.md)

[**NDIS\_WWAN\_服务\_激活**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation)

[ **\_WWAN\_服务\_激活的 NDIS\_状态**](ndis-status-wwan-service-activation.md)

[MB 服务检测和激活](https://docs.microsoft.com/windows-hardware/drivers/network/mb-service-detection-and-activation)

 

 




