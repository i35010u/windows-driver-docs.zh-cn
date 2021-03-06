---
title: OID_QOS_CURRENT_CAPABILITIES
description: 过量驱动程序发出对象标识符 (OID) 查询请求 OID_QOS_CURRENT_CAPABILITIES 获取当前启用的 NDIS 服务质量 (QoS) 网络适配器的硬件功能。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_QOS_CURRENT_CAPABILITIES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e7d7d49822b5c14c30b58f70c7d2bf7866ec3e71
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248889"
---
# <a name="oid_qos_current_capabilities"></a>OID \_ QOS \_ 当前 \_ 功能


过量驱动程序发出 (OID 的对象标识符) 请求 OID \_ QOS \_ 当前 \_ 功能，以获取网络适配器的当前启用的 NDIS 服务 (QOS) 硬件功能。

成功从 OID 查询请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ QOS \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)结构的指针。

**注意**  此 OID 查询请求由支持 IEEE 802.1 数据中心桥接 (DCB) 接口的微型端口驱动程序的 NDIS 处理。

 

<a name="remarks"></a>备注
-------

在调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，微型端口驱动程序会注册网络适配器的当前启用的 NDIS QoS 硬件功能。 驱动程序会按照以下步骤注册这些功能：

1.  驱动程序使用启用的 QoS 硬件功能初始化 [**NDIS \_ QOS \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities) 结构。

2.  驱动程序将 [**ndis \_ 微型端口 \_ 适配器 \_ 硬件 \_ 辅助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构的 **CurrentQosCapabilities** 成员设置为指向 [**NDIS \_ QOS \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)结构的指针。

3.  然后，小型端口驱动程序将调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 函数，并将 *MiniportAttributes* 参数设置为指向 [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes) 结构的指针。

**注意**  在绑定或附加操作期间，NDIS 不会将网络适配器的当前启用的 NDIS QoS 硬件功能报告给过量的协议和筛选器驱动程序。

 

有关如何注册 NDIS QoS 功能的详细信息，请参阅 [注册 Ndis Qos 功能](./registering-ndis-qos-capabilities.md)。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 \_ \_ 针对微型端口驱动程序的 oid QOS 当前功能请求的 oid 查询请求 \_ ，并返回以下状态代码之一。

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
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>微型端口驱动程序不支持 NDIS QoS 接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof (<a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities" data-raw-source="[&lt;strong&gt;NDIS_QOS_CAPABILITIES&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)"><strong>NDIS_QOS_CAPABILITIES</strong></a>) 。 NDIS 设置 <strong>数据。QUERY_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

[**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 辅助 \_ 特性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ QOS \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)

