---
title: OID_NIC_SWITCH_CURRENT_CAPABILITIES
description: 基础驱动程序发出的对象标识符 (OID) 查询请求的 OID_NIC_SWITCH_CURRENT_CAPABILITIES 以获取当前已启用的硬件功能的网络适配器中的 NIC 交换机。
ms.assetid: 529dc5d5-9b84-4891-9e7a-1f9f7850c6d7
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_CURRENT_CAPABILITIES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ab0ad88bd45f9b5f01eb45cbee6622fb4c69b27f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383673"
---
# <a name="oidnicswitchcurrentcapabilities"></a>OID\_NIC\_交换机\_当前\_功能


基础驱动程序将发出对象标识符 (OID) 查询请求的 OID\_NIC\_切换\_当前\_功能来获取当前已启用的硬件功能的 NIC 的网络适配器中，请切换.

从 OID 查询请求，成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_NIC\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构。

<a name="remarks"></a>备注
-------

从开始 NDIS 6.20，微型端口驱动程序提供的网络适配器上的当前已启用的 NIC 交换机硬件功能时其[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)调用函数。 该驱动程序初始化[ **NDIS\_NIC\_切换\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构与 NIC 切换硬件功能和集**CurrentNicSwitchCapabilities**的成员[ **NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)指向的结构**NDIS\_NIC\_交换机\_功能**结构。 然后调用微型端口驱动程序[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)函数和集*MiniportAttributes*参数指向的**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**结构。

**请注意**  从 NDIS 6.30 开始，支持单根 I/O 虚拟化 (SR-IOV) 接口的微型端口驱动程序必须注册的 NIC 开关已启用的硬件功能。 驱动程序通过调用注册这些功能[ **NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)。

 

基础协议和筛选器驱动程序无需发出 OID 查询请求的 OID\_NIC\_交换机\_当前\_功能。 NDIS 按以下方式提供对这些驱动程序的网络适配器的当前已启用的 NIC 交换机硬件功能：

-   NDIS 报告当前已启用的 NIC 交换机硬件功能的基础的网络适配器到过量协议中的驱动程序**NicSwitchCapabilities**的成员[ **NDIS\_将绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)绑定操作过程中的结构。

-   NDIS 报告当前已启用的 NIC 交换机硬件功能的基础的网络适配器到过量中的筛选器驱动程序**NicSwitchCapabilities**的成员[ **NDIS\_筛选器\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)在附加操作期间的结构。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID 查询请求的 OID\_NIC\_交换机\_当前\_微型端口驱动程序的功能请求。 驱动程序将不会颁发此 OID 请求。

NDIS 时处理 OID\_NIC\_交换机\_当前\_功能请求，它将返回以下状态代码之一：

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
<td><p>请求已成功完成。 <strong>InformationBuffer</strong>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"> <strong>NDIS_NIC_SWITCH_CAPABILITIES</strong> </a>结构。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>微型端口驱动程序不支持的单个根 I/O 虚拟化 (SR-IOV) 接口，或未启用要使用的界面。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度不超过 sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"><strong>NDIS_NIC_SWITCH_CAPABILITIES</strong></a>)。 微型端口驱动程序必须设置<strong>数据。QUERY_INFORMATION。BytesNeeded</strong>中的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>请求由于其他原因而失败。</p></td>
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
<td><p>支持 NDIS 6.20 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_BIND\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_FILTER\_ATTACH\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)

[**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NDIS\_NIC\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)

[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

 

 




