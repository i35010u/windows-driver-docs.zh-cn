---
title: OID_NIC_SWITCH_VPORT_PARAMETERS
description: 基础驱动程序可以获取支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器已创建的 NIC 交换机上的虚拟端口 (VPort) 的参数。
ms.assetid: B22C760E-F2B0-4774-A532-4044C679CD64
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_VPORT_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 74d51bf13d95e4d575b6e2e74cdb3219012d7bcf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383255"
---
# <a name="oidnicswitchvportparameters"></a>OID\_NIC\_交换机\_VPORT\_参数


基础驱动程序可以获取支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器已创建的 NIC 交换机上的虚拟端口 (VPort) 的参数。 驱动程序将发出对象标识符 (OID) 方法请求的 OID\_NIC\_交换机\_VPORT\_参数来获取这些参数。

过量驱动程序问题 OID 设置请求的 OID\_NIC\_切换\_VPORT\_参数来设置附加到网络适配器的 NIC 交换机指定 VPort 的配置参数。 这些 OID 集请求颁发给微型端口驱动程序的网络适配器的 PCI Express (PCIe) 物理函数 (PF)。 这些 OID 集请求所需的支持的单个根 I/O 虚拟化 (SR-IOV) 接口的 PF 微型端口驱动程序。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构。

基础驱动程序指定的 OID 方法 VPort 或通过设置集请求**VPortId**的成员[ **NDIS\_NIC\_开关\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构 VPort 与关联的标识符。 基础驱动程序将获取通过以下方式之一的 VPort 标识符：

-   从上一个 OID 方法请求的[OID\_NIC\_交换机\_创建\_VPORT](oid-nic-switch-create-vport.md)。

-   从上一个 OID 方法请求的[OID\_NIC\_交换机\_枚举\_VPORTS](oid-nic-switch-enum-vports.md)。

<a name="remarks"></a>备注
-------

OID\_NIC\_交换机\_VPORT\_可以使用参数中任意一种[OID 方法请求](#oid-method-requests)或[OID 设置请求](#oid-set-requests)。

### <a href="" id="oid-method-requests"></a>处理 OID 方法请求的 OID\_NIC\_交换机\_VPORT\_参数

基础驱动程序发出 OID 方法请求的 OID\_NIC\_切换\_VPORT\_查询连接到网络适配器的 NIC 切换 VPort 的当前配置参数的参数。 基础驱动程序通过设置来指定查询 VPort **VPortId**的成员[ **NDIS\_NIC\_开关\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters) VPort 标识符的结构。

NDIS 处理 OID 方法请求的 OID\_NIC\_交换机\_VPORT\_微型端口驱动程序的参数。 NDIS 返回它从的以前的 OID 请求获取的信息[OID\_NIC\_交换机\_创建\_VPORT](oid-nic-switch-create-vport.md)并[OID\_NIC\_交换机\_ENUM\_VPORTS](oid-nic-switch-enum-vports.md)。

通过 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构。 此结构包含指定的交换机的配置参数。

有关详细信息，请参阅[查询的虚拟端口参数](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-parameters-of-a-virtual-port)。

### <a href="" id="oid-set-requests"></a>处理 OID 设置请求的 OID\_NIC\_交换机\_VPORT\_参数

过量驱动程序问题 OID 设置请求的 OID\_NIC\_切换\_VPORT\_参数以更改连接到网络适配器的 NIC 切换 VPort 的当前配置参数。 此 OID 请求可用于更新为非默认 VPorts 或默认的参数。

可以更改仅有限 VPort 的配置参数。 基础驱动程序指定要更改设置的以下成员的参数[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构：

1.  **VPortId**成员设置为其参数将会更改的 VPort 的标识符。

2.  合适的 NDIS\_NIC\_交换机\_VPORT\_参数\_*Xxx*\_设置已更改标志**标志**成员。 成员[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构只能如果相应 NDIS 更改\_NIC\_交换机\_参数\_*Xxx*\_中 Ntddndis.h 定义已更改的标志。

3.  对应成员[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构使用 VPort 配置设置要更改的参数。

PF 后微型端口驱动程序收到 OID 集请求的 OID\_NIC\_交换机\_VPORT\_参数，该驱动程序配置硬件使用的配置参数。 该驱动程序只能更改这些配置参数标识的 NDIS\_NIC\_交换机\_VPORT\_参数\_*Xxx*\_已更改在标记**标志**的成员[ **NDIS\_NIC\_开关\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构。

有关详细信息，请参阅[设置的虚拟端口参数](https://docs.microsoft.com/windows-hardware/drivers/network/setting-the-parameters-of-a-virtual-port)。

### <a name="return-status-codes"></a>返回状态代码

NDIS 或 PF 微型端口驱动程序返回集或方法的以下状态代码的 OID 的 OID 请求\_NIC\_交换机\_VPORT\_参数。

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
<td><p>PF 微型端口驱动程序不支持的单个根 I/O 虚拟化 (SR-IOV) 接口，或未启用要使用的界面。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>一个或多个的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VPORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)"> <strong>NDIS_NIC_SWITCH_VPORT_PARAMETERS</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 或 PF 微型端口驱动程序设置<strong>数据。METHOD_INFORMATION。BytesNeeded</strong> （对于 OID 方法请求） 的成员或<strong>数据。SET_INFORMATION。BytesNeeded</strong> （对于 OID 集请求） 中的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
</tr>
<tr class="odd">
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
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS\_NIC\_SWITCH\_VPORT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)

[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[OID\_NIC\_SWITCH\_CREATE\_VPORT](oid-nic-switch-create-vport.md)

[OID\_NIC\_交换机\_枚举\_VPORTS](oid-nic-switch-enum-vports.md)

 

 




