---
title: OID_QOS_PARAMETERS
description: 数据中心桥接（DCB）组件（Msdcb）发出 OID_QOS_PARAMETERS 的对象标识符（OID）方法请求，以在网络适配器上配置本地 NDIS 服务质量（QoS）参数。
ms.assetid: 1CA97C8A-8F5B-4AB2-B68E-DF1FA772C08F
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_QOS_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f7c295ef30da68bc07fb353789dc79027e3ad270
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844026"
---
# <a name="oid_qos_parameters"></a>OID\_QOS\_参数


数据中心桥接（DCB）组件（Msdcb）发出 OID\_QOS\_参数的对象标识符（OID）方法请求，以便在网络适配器上配置本地 NDIS 服务质量（QoS）参数。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的指针。

**注意** 对于支持 IEEE 802.1 数据中心桥接（DCB）接口的 NDIS QoS 的微型端口驱动程序，此 OID 方法请求是必需的。



<a name="remarks"></a>备注
-------

微型端口驱动程序通过 oid\_QOS 方法请求\_参数获取本地 NDIS QoS 参数。 这些参数定义网络适配器如何确定传输或*传出*数据包的优先级。 有关这些参数的详细信息，请参阅 " [NDIS QoS 参数概述](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-ndis-qos-parameters)"。

**注意** 只有 DCB 组件可以\_QOS\_参数发出 oid 方法请求。 过量协议或筛选器驱动程序不得颁发此 OID。 有关 DCB 组件的详细信息，请参阅[用于数据中心桥接的 NDIS QoS 体系结构](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-qos-architecture-for-data-center-bridging)。



在以下情况下，DCB 组件将\_QOS\_参数请求发出 OID：

-   系统管理员安装或卸载 Microsoft DCB 服务器功能。

    有关 DCB 服务器功能的详细信息，请参阅[系统提供的 DCB 组件](https://docs.microsoft.com/windows-hardware/drivers/network/system-provided-dcb-components)。

-   当功能仍然安装时，系统管理员启用或禁用 DCB 服务器功能。

-   系统管理员更改 DCB 服务器功能参数中的任何一个。

-   安装 DCB 服务器功能时，操作系统将启动或重新启动。

当微型端口驱动程序处理 OID\_QOS\_参数的 OID 方法请求时，必须遵循以下准则：

-   微型端口驱动程序将[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构中的数据复制到其本地 NDIS QOS 参数的缓存中。 然后，该驱动程序将基于其本地 NDIS QoS 参数的缓存及其从远程对等机接收的 NDIS QoS 参数缓存来解析其操作的 NDIS QoS 参数。

    有关微型端口驱动程序如何解析其操作参数的详细信息，请参阅[解决操作 NDIS QoS 参数](https://docs.microsoft.com/windows-hardware/drivers/network/resolving-operational-ndis-qos-parameters)。

-   微型端口驱动程序不得修改[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构中包含的任何数据。 驱动程序必须完成 OID 方法请求并返回**NDIS\_QOS\_参数**结构中的原始数据。

-   **NDIS\_QOS\_参数\_愿意**标志指定微型端口驱动程序是启用还是禁用本地数据中心桥接 EXCHANGE （DCBX）的状态。 驱动程序通过以下方式处理此标志：

    -   如果设置了此标志，微型端口驱动程序必须启用本地 DCBX。 这允许用 QoS 设置对驱动程序进行远程配置。 在这种情况下，驱动程序将根据远程 QoS 参数解析其操作 QoS 参数。 微型端口驱动程序还可以根据独立硬件供应商（IHV）定义的任何专有 QoS 设置来解析其操作 QoS 参数。

    -   如果未设置此标志，微型端口驱动程序必须禁用本地 DCBX。 这允许驱动程序从其本地 QoS 参数而不是远程 QoS 参数解析其操作 QoS 参数。 微型端口驱动程序还必须禁用或重写未设置相关**NDIS\_qos\_参数\_*XXX*\_配置**标志的任何本地 QoS 参数。

        例如，微型端口驱动程序可以为由 IHV 定义的 QoS 参数覆盖未配置的本地 QoS 参数及其专有设置。 如果没有使用**NDIS\_qos\_参数\_*XXX*\_配置**的标志指定的本地 QoS 参数没有专用设置，则驱动程序必须在网络上禁用这些 qos 参数的使用适配器.

        **注意** 如果已配置的本地 QoS 参数泄露由网络适配器上启用的协议或技术使用的 QoS 参数，则该驱动程序还可以覆盖这些参数。 例如，如果光纤通道通过以太网（FCoE）协议为网络适配器启用了远程启动，则驱动程序可以替代本地 QoS 参数。

    有关本地 DCBX 适用状态的详细信息，请参阅[管理本地 DCBX 适用的状态](https://docs.microsoft.com/windows-hardware/drivers/network/managing-the-local-dcbx-willing-state)。

有关微型端口驱动程序如何替代本地 QoS 参数的详细信息，请参阅[管理 NDIS Qos 参数](https://docs.microsoft.com/windows-hardware/drivers/network/managing-ndis-qos--parameters)。

**注意** 替代本地 QoS 参数不应导致微型\_QOS 方法的 oid 方法请求失败\_参数。

有关微型端口驱动程序如何管理本地 QoS 参数的详细信息，请参阅[设置本地 NDIS Qos 参数](https://docs.microsoft.com/windows-hardware/drivers/network/setting-local-ndis-qos-parameters)。

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序返回以下状态代码之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_PENDING</p></td>
<td><p>OID 请求正在等待完成。 当微型端口驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a>时，在请求完成后，NDIS 会将最终的状态代码和结果传递给调用方的 OID 请求完成处理程序。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>微型端口驱动程序不支持 NDIS QoS 接口。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>一个或多个<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)"><strong>NDIS_QOS_PARAMETERS</strong></a>结构成员包含不正确的值。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于<strong>sizeof</strong>（<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)"><strong>NDIS_QOS_PARAMETERS</strong></a>）。 NDIS 设置<strong>数据。QUERY_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>由于其他原因，请求失败。</p></td>
</tr>
</tbody>
</table>



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
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_QOS\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)

[**NDIS\_状态\_QOS\_操作\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)

[**NDIS\_状态\_QOS\_远程\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)








