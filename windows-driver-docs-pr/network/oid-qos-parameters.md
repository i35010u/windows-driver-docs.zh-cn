---
title: OID_QOS_PARAMETERS
description: 数据中心桥接 (DCB) 组件 (Msdcb.sys) 发出对象标识符 (OID) OID_QOS_PARAMETERS 的 (方法请求，以配置网络适配器上的本地 NDIS 服务) QoS 参数。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_QOS_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b15e88b52629ccc46e475b8d8767fa6fddbb60e1
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248869"
---
# <a name="oid_qos_parameters"></a>OID \_ QOS \_ 参数


数据中心桥接 (DCB) 组件 (Msdcb.sys) 发出对象标识符 (OID) OID (方法请求 OID \_ qos \_ 参数，以在网络适配器上配置本地 NDIS 服务) QOS 参数。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的指针。

**注意**  对于支持 IEEE 802.1 数据中心桥接 (DCB) 接口的 NDIS QoS 的微型端口驱动程序，此 OID 方法请求是必需的。



<a name="remarks"></a>备注
-------

微型端口驱动程序通过 oid qos 参数的 OID 方法请求获取本地 NDIS QoS 参数 \_ \_ 。 这些参数定义网络适配器如何确定传输或 *传出* 数据包的优先级。 有关这些参数的详细信息，请参阅 " [NDIS QoS 参数概述](./overview-of-ndis-qos-parameters.md)"。

**注意**  只有 DCB 组件可以发出 OID QOS 参数的 OID 方法请求 \_ \_ 。 过量协议或筛选器驱动程序不得颁发此 OID。 有关 DCB 组件的详细信息，请参阅 [用于数据中心桥接的 NDIS QoS 体系结构](./ndis-qos-architecture-for-data-center-bridging.md)。



在下列情况下，DCB 组件会发出 OID \_ QOS \_ 参数请求：

-   系统管理员安装或卸载 Microsoft DCB 服务器功能。

    有关 DCB 服务器功能的详细信息，请参阅 [系统提供的 DCB 组件](./system-provided-dcb-components.md)。

-   当功能仍然安装时，系统管理员启用或禁用 DCB 服务器功能。

-   系统管理员更改 DCB 服务器功能参数中的任何一个。

-   安装 DCB 服务器功能时，操作系统将启动或重新启动。

当微型端口驱动程序处理 OID QOS 参数的 OID 方法请求时 \_ \_ ，必须遵循以下准则：

-   微型端口驱动程序将 [**NDIS \_ qos \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构内的数据复制到其本地 NDIS qos 参数的缓存中。 然后，该驱动程序将基于其本地 NDIS QoS 参数的缓存及其从远程对等机接收的 NDIS QoS 参数缓存来解析其操作的 NDIS QoS 参数。

    有关微型端口驱动程序如何解析其操作参数的详细信息，请参阅 [解决操作 NDIS QoS 参数](./resolving-operational-ndis-qos-parameters.md)。

-   微型端口驱动程序不得修改 [**NDIS \_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构中包含的任何数据。 驱动程序必须完成 OID 方法请求并返回 **NDIS \_ QOS \_ 参数** 结构中的原始数据。

-   **NDIS \_ QOS 参数 \_ " \_ 愿意**" 标志指定微型端口驱动程序是启用还是禁用本地数据中心桥接 Exchange (DCBX) "愿意" 状态。 驱动程序通过以下方式处理此标志：

    -   如果设置了此标志，微型端口驱动程序必须启用本地 DCBX。 这允许用 QoS 设置对驱动程序进行远程配置。 在这种情况下，驱动程序将根据远程 QoS 参数解析其操作 QoS 参数。 微型端口驱动程序还可以根据独立硬件供应商 (IHV) 定义的任何专有 QoS 设置来解析其操作 QoS 参数。

    -   如果未设置此标志，微型端口驱动程序必须禁用本地 DCBX。 这允许驱动程序从其本地 QoS 参数而不是远程 QoS 参数解析其操作 QoS 参数。 微型端口驱动程序还必须禁用或重写未设置相关 **NDIS \_ qos \_ 参数 \_ *Xxx* \_ 配置** 标志的任何本地 QoS 参数。

        例如，微型端口驱动程序可以为由 IHV 定义的 QoS 参数覆盖未配置的本地 QoS 参数及其专有设置。 如果没有使用 **NDIS \_ qos \_ 参数 \_ *Xxx* \_ 配置** 标志指定的本地 QoS 参数的专用设置，则驱动程序必须在网络适配器上禁用这些 qos 参数。

        **注意**  如果已配置的本地 QoS 参数泄露由网络适配器上启用的协议或技术使用的 QoS 参数，则该驱动程序还可以覆盖这些参数。 例如，如果光纤通道通过以太网 (FCoE) 协议为网络适配器启用了远程启动，则驱动程序可以替代本地 QoS 参数。

    有关本地 DCBX 适用状态的详细信息，请参阅 [管理本地 DCBX 适用的状态](./managing-the-local-dcbx-willing-state.md)。

有关微型端口驱动程序如何替代本地 QoS 参数的详细信息，请参阅 [管理 NDIS Qos 参数](overview-of-ndis-qos-parameters.md)。

**注意**  替代本地 QoS 参数不应导致微型端口驱动程序无法通过 oid QoS 参数的 OID 方法 \_ 请求 \_ 。

有关微型端口驱动程序如何管理本地 QoS 参数的详细信息，请参阅 [设置本地 NDIS Qos 参数](./setting-local-ndis-qos-parameters.md)。

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
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_PENDING</p></td>
<td><p>OID 请求正在等待完成。 当微型端口驱动程序调用 <a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a>时，在请求完成后，NDIS 会将最终的状态代码和结果传递给调用方的 OID 请求完成处理程序。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>微型端口驱动程序不支持 NDIS QoS 接口。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)"><strong>NDIS_QOS_PARAMETERS</strong></a>结构的一个或多个成员包含不正确的值。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 <strong>sizeof</strong> (<a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)"><strong>NDIS_QOS_PARAMETERS</strong></a>) 。 NDIS 设置 <strong>数据。QUERY_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
<td><p>Version</p></td>
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NdisMOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ QOS \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)

[**NDIS \_ 状态 \_ QOS \_ 操作 \_ 参数 \_ 更改**](./ndis-status-qos-operational-parameters-change.md)

[**NDIS \_ 状态 \_ QOS \_ 远程 \_ 参数 \_ 更改**](./ndis-status-qos-remote-parameters-change.md)
