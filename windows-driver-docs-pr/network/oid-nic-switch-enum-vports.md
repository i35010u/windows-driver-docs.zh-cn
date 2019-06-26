---
title: OID_NIC_SWITCH_ENUM_VPORTS
description: 基础驱动程序或用户模式应用程序发出的对象标识符 (OID) 方法请求的 OID_NIC_SWITCH_ENUM_VPORTS 以获取数组。
ms.assetid: 4B9587E0-3CA9-46AF-A80E-969E6D563922
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_ENUM_VPORTS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9735448720d47f43b70b6072dd7c949bdd82699d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383661"
---
# <a name="oidnicswitchenumvports"></a>OID\_NIC\_交换机\_枚举\_VPORTS


基础驱动程序或用户模式应用程序颁发的 OID 的对象标识符 (OID) 方法请求\_NIC\_交换机\_枚举\_VPORTS 以获取数组。 数组中的每个元素指定网络适配器的 NIC 交换机已创建的虚拟端口 (VPort) 的特性。

通过此 OID 查询请求的成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含指向包含以下各项的缓冲区的指针：

-   [ **NDIS\_NIC\_交换机\_VPORT\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)结构，用于定义数组中元素数。

-   一个数组[ **NDIS\_NIC\_交换机\_VPORT\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)结构。 每个这些结构包含有关 VPort 网络适配器的 NIC 交换机上的信息。

    **请注意**  如果在网络适配器上未不创建任何 VPorts，驱动程序设置**NumElements**的成员[ **NDIS\_NIC\_开关\_VPORT\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)为零，并无结构[ **NDIS\_NIC\_交换机\_VPORT\_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)返回结构。

     

<a name="remarks"></a>备注
-------

基础驱动程序和用户模式应用程序颁发的 OID 的 OID 查询请求\_NIC\_切换\_枚举\_VPORTS 枚举网络适配器的 NIC 交换机分配 VPorts。

驱动程序或应用程序发出 OID 请求之前，必须将格式化[ **NDIS\_NIC\_交换机\_VPORT\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)随请求一起传递的结构。 驱动程序或应用程序初始化时，必须遵循这些准则**NDIS\_NIC\_交换机\_VPORT\_信息\_数组**结构：

-   如果 NDIS\_NIC\_交换机\_VPORT\_信息\_数组\_枚举\_ON\_特定\_中设置了开关标志**标志**成员，则返回的信息为所有 VPorts 都创建指定 NIC 交换机上。 通过指定 NIC 开关**SwitchId**该结构的成员。

    **请注意**  从 Windows Server 2012 开始，SR-IOV 接口上的网络适配器支持仅默认 NIC 切换。 无论在中设置的标志**标志**成员**SwitchId**成员必须设置为 NDIS\_默认\_开关\_id。

     

-   如果 NDIS\_NIC\_交换机\_VPORT\_信息\_数组\_枚举\_ON\_特定\_中设置函数标志**标志**成员，则返回的信息为所有 VPorts 都附加到指定 PCI Express (PCIe) 物理函数 (PF) 或虚拟函数 (VF) 上的网络适配器。 通过指定 PF 或 VF **AttachedFunctionId**该结构的成员。

    如果**AttachedFunctionId**成员设置为 NDIS\_PF\_函数\_ID，用于附加到网络适配器的 PF.的所有 VPorts，包括默认 VPort，返回的信息 如果**AttachedFunctionId**成员设置为有效的 VF 标识符、 到指定 VF 为所有 VPorts 返回信息。

    **请注意**  从 Windows Server 2012，只有一个非默认 VPort 可以附加到 VF 开始。 但是，可以将多个 VPorts （包括默认 VPort） 附加到 PF.

     

-   如果**标志**成员设置为零，对于所有 VPorts 都附加到 PF 或 VF 上的网络适配器，将返回信息。 在本示例中的值**SwitchId**并**AttachedFunctionId**将被忽略。

有关详细信息，请参阅[枚举网络适配器上的虚拟端口](https://docs.microsoft.com/windows-hardware/drivers/network/enumerating-virtual-ports-on-a-network-adapter)。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID 方法请求的 OID\_NIC\_交换机\_枚举\_VPORTS 微型端口驱动程序的请求。 驱动程序将不会颁发此 OID 请求。

NDIS 时处理 OID\_NIC\_交换机\_枚举\_VPORTS 请求，它将返回以下状态代码之一：

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
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>微型端口驱动程序不支持的单个根 I/O 虚拟化 (SR-IOV) 接口，或未启用要使用的界面。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>一个或多个的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_INFO_ARRAY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)"> <strong>NDIS_NIC_SWITCH_VF_INFO_ARRAY</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 集<strong>数据。METHOD_INFORMATION。BytesNeeded</strong>中的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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
[**NDIS\_NIC\_交换机\_VPORT\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)

[**NDIS\_NIC\_交换机\_VPORT\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)

[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[OID\_NIC\_SWITCH\_CREATE\_SWITCH](oid-nic-switch-create-switch.md)

[OID\_NIC\_SWITCH\_PARAMETERS](oid-nic-switch-parameters.md)

 

 




