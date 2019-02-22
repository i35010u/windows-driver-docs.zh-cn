---
title: OID_NIC_SWITCH_CREATE_VPORT
description: 基础驱动程序发出的对象标识符 (OID) 方法请求 OID_NIC_SWITCH_CREATE_VPORT 的网络适配器的 NIC 交换机上创建非默认虚拟端口 (VPort)。
ms.assetid: 31109117-2242-40E0-B215-0FAE014B2035
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_CREATE_VPORT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 742bee63784913086d9e777607e401369c4c5ff1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521877"
---
# <a name="oidnicswitchcreatevport"></a>OID\_NIC\_交换机\_创建\_VPORT


基础驱动程序发出的 OID 的对象标识符 (OID) 方法请求\_NIC\_切换\_创建\_VPORT 网络适配器的 NIC 交换机上创建非默认虚拟端口 (VPort)。 此 OID 方法请求还将创建的 VPort 附加到网络适配器的 PCI Express (PCIe) 物理函数 (PF) 或以前分配 PCIe 虚拟函数 (VF)。

基础驱动程序发出此 OID 方法请求到微型端口驱动程序的网络适配器 PF. 此 OID 方法请求是必需的支持的单个根 I/O 虚拟化 (SR-IOV) 接口的 PF 微型端口驱动程序。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)结构。

<a name="remarks"></a>备注
-------

基础驱动程序初始化[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)的配置信息的结构有关非默认 VPort 创建。 配置信息包括向其附加 VPort 非默认和数量的队列对的非默认 VPort PCIe 函数。

PF 微型端口驱动程序发出 OID 请求，该驱动程序会分配与指定非默认 VPort 关联的硬件和软件资源。 通过返回 NDIS 组件时 PF 微型端口驱动程序的所有资源都分配成功后，已成功完成 OID\_状态\_从成功[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416).

如果 OID\_NIC\_交换机\_创建\_VPORT 请求成功完成，PF 微型端口驱动程序和基础驱动程序必须保留**VPortId**的非默认值VPort 用于后续操作。 **VPortId**进行这些操作时使用值：

-   使用 NDIS 和基础驱动程序**VPortId**值以标识非默认中连续 OID VPort 请求与此 VPort 相关如[OID\_NIC\_开关\_VPORT\_参数](oid-nic-switch-vport-parameters.md)并[OID\_NIC\_开关\_删除\_VPORT](oid-nic-switch-delete-vport.md)。

-   在发送操作期间指定 NDIS **VPortId**值以标识从其发送数据包 VPort。 带外 (OOB) 中指定此值[ **NDIS\_NET\_缓冲区\_列表\_筛选\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff566567)的数据[NET\_缓冲区\_列表](https://msdn.microsoft.com/library/windows/hardware/ff568412)结构。

-   在接收操作，PF 微型端口驱动程序指定**VPortId**数据包将转发到的值。 此值还指定在 OOB [ **NDIS\_NET\_缓冲区\_列表\_筛选\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff566567) 数据[NET\_缓冲区\_列表](https://msdn.microsoft.com/library/windows/hardware/ff568412)结构。

有关详细信息，请参阅[创建虚拟端口](https://msdn.microsoft.com/library/windows/hardware/hh439412)。

**请注意**  VPort 始终存在，并且不是默认值创建但 OID 的 OID 请求\_NIC\_交换机\_创建\_VPORT。 默认 VPort 具有标识符的 NDIS\_默认\_VPORT\_id。 当 PF 微型端口驱动程序创建一个 NIC 开关时，该驱动程序会自动默认 VPort 附加到网络适配器的 PF。

 

### <a name="return-status-codes"></a>返回状态代码

NDIS 或 PF 微型端口驱动程序返回一个 OID 的 OID 方法请求的以下状态代码\_NIC\_交换机\_创建\_开关。

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
<td><p>PF 微型端口驱动程序不支持 SR-IOV 接口，或未启用要使用的界面。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>一个或多个的成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh451597" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VPORT_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451597)"> <strong>NDIS_NIC_SWITCH_VPORT_PARAMETERS</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度不超过 sizeof (<a href="https://msdn.microsoft.com/library/windows/hardware/hh451597" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VPORT_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451597)"><strong>NDIS_NIC_SWITCH_VPORT_PARAMETERS</strong></a>)。 PF 微型端口驱动程序必须设置<strong>数据。METHOD_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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
<td><p>版本</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[*MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416)

[**NDIS\_NIC\_SWITCH\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451587)

[**NDIS\_NIC\_SWITCH\_VPORT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451597)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[NET\_BUFFER\_LIST](https://msdn.microsoft.com/library/windows/hardware/ff568412)

[OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_交换机\_删除\_VPORT](oid-nic-switch-delete-vport.md)

[OID\_NIC\_SWITCH\_PARAMETERS](oid-nic-switch-parameters.md)

[OID\_NIC\_交换机\_VPORT\_参数](oid-nic-switch-vport-parameters.md)

 

 




