---
title: OID_NIC_SWITCH_PARAMETERS
description: 基础驱动程序发出的对象标识符 (OID) 方法请求的 OID_NIC_SWITCH_PARAMETERS 获取指定的 NIC 交换机的网络适配器上的当前配置参数。
ms.assetid: 3F2FF2C0-8710-4243-8583-CD80F244FCFB
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2bc175478337d37ac0008672b9a1fd67dde191a4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380843"
---
# <a name="oidnicswitchparameters"></a>OID\_NIC\_交换机\_参数


基础驱动程序发出的 OID 的对象标识符 (OID) 方法请求\_NIC\_切换\_参数来获取当前的配置参数指定 NIC 的网络适配器上切换。 NDIS 处理微型端口驱动程序这些 OID 方法请求。

过量驱动程序问题 OID 设置请求的 OID\_NIC\_切换\_网络适配器上切换参数来设置指定 NIC 的配置参数。 这些 OID 集请求颁发给微型端口驱动程序的网络适配器的 PCI Express (PCIe) 物理函数 (PF)。 这些 OID 集请求所需的支持的单个根 I/O 虚拟化 (SR-IOV) 接口的 PF 微型端口驱动程序。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_NIC\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构。

基础驱动程序指定的 OID 方法的 NIC 交换机或通过设置集请求**SwitchId**的成员[ **NDIS\_NIC\_切换\_参数** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)交换机标识符的结构。 基础驱动程序将获取通过以下方式之一的交换机标识符：

-   从上一个 OID 方法请求的[OID\_NIC\_交换机\_枚举\_开关](oid-nic-switch-enum-switches.md)。

-   从**NicSwitchArray**的成员[ **NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)结构。 NDIS 将指针传递到此结构*BindParameters*的参数[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)函数。

-   从**NicSwitchArray**的成员[ **NDIS\_筛选器\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。 NDIS 将指针传递到此结构*AttachParameters*的参数[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)函数。

**请注意**  从 Windows Server 2012 开始，Windows 上的网络适配器支持仅默认 NIC 切换。 **SwitchId**的成员[ **NDIS\_NIC\_开关\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构必须设置为 NDIS\_默认值\_交换机\_id。

 

<a name="remarks"></a>备注
-------

基础驱动程序将发出 OID\_NIC\_交换机\_参数请求如下所示：

-   基础驱动程序将发出 OID 的 OID 方法请求\_NIC\_切换\_参数来获取指定 NIC 开关的当前参数。 有关详细信息，请参阅[查询的 NIC 开关参数](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-parameters-of-a-nic-switch)。

    **请注意**  NDIS 处理 OID 方法请求的 OID\_NIC\_交换机\_PF 微型端口驱动程序的参数。

     

-   基础驱动程序将发出 OID 的 OID 集请求\_NIC\_切换\_更改指定 NIC 开关的当前参数的参数。 有关详细信息，请参阅[设置的 NIC 开关参数](https://docs.microsoft.com/windows-hardware/drivers/network/setting-the-parameters-of-a-nic-switch)。

    **请注意**  PF 微型端口驱动程序处理 OID 集请求的 OID\_NIC\_交换机\_参数。

     

### <a name="return-status-codes"></a>返回状态代码

NDIS 或 PF 微型端口驱动程序返回的集或方法的以下状态代码的 OID 的 OID 请求\_NIC\_交换机\_参数。

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
<td><p>一个或多个的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)"> <strong>NDIS_NIC_SWITCH_PARAMETERS</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 或 PF 微型端口驱动程序设置<strong>数据。METHOD_INFORMATION。BytesNeeded</strong> （对于 OID 方法请求） 的成员或<strong>数据。SET_INFORMATION。BytesNeeded</strong> （对于 OID 集请求） 中的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_REINIT_REQUIRED</p></td>
<td><p>PF 微型端口驱动程序要求将更改应用到 NIC 交换机的网络适配器进行重新初始化。</p></td>
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
[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)

[**NDIS\_BIND\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_FILTER\_ATTACH\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)

[**NDIS\_NIC\_SWITCH\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)

[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[OID\_NIC\_SWITCH\_CREATE\_SWITCH](oid-nic-switch-create-switch.md)

[OID\_NIC\_SWITCH\_ENUM\_SWITCHES](oid-nic-switch-enum-switches.md)

[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)

 

 




