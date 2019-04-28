---
title: OID_NIC_SWITCH_VF_PARAMETERS
description: 基础驱动程序或用户模式应用程序发出的对象标识符 (OID) 方法请求的 OID_NIC_SWITCH_VF_PARAMETERS 以获取当前的配置参数的 PCI Express (PCIe) 虚拟函数 (VF) 上的网络适配器。
ms.assetid: DF08B0BA-6D86-4C4F-AC38-8A401F097925
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_VF_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 69a7bdb5f9f3050aca78adcf3b7d207a44abae6d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350959"
---
# <a name="oidnicswitchvfparameters"></a>OID\_NIC\_SWITCH\_VF\_PARAMETERS


基础驱动程序或用户模式应用程序颁发的 OID 的对象标识符 (OID) 方法请求\_NIC\_交换机\_VF\_参数来获取当前的配置参数的 PCI Express (PCIe)虚拟函数 (VF) 上的网络适配器。 已通过 OID 方法请求的分配的资源的 VFs [OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)可以通过 OIDOID方法请求查询\_NIC\_交换机\_VF\_参数。

NDIS 处理 OID 方法请求的 OID\_NIC\_交换机\_VF\_微型端口驱动程序的参数。

发出 OID 方法请求后， **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含的指针[ **NDIS\_NIC\_交换机\_VF\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451593)结构。

<a name="remarks"></a>备注
-------

过量的驱动程序或用户模式应用程序通过设置指定查询 VF **VFId**的成员[ **NDIS\_NIC\_开关\_VF\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451593)结构为 VF 的标识符。 基础驱动程序或应用程序中获取 VF 标识符通过以下方式之一：

-   通过发出的 OID 方法请求[OID\_NIC\_交换机\_枚举\_VFS](oid-nic-switch-enum-vfs.md)。

    如果已成功完成此 OID 请求，则基础驱动程序或用户模式应用程序接收所有 VFs 上的网络适配器分配的列表。 在列表中的每个元素均[ **NDIS\_NIC\_交换机\_VF\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451591)的结构，其中指定VF标识符**VFId**成员。

-   通过发出的 OID 方法请求[OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)。

    如果已成功完成此 OID 请求，则基础驱动程序接收的标识符中新创建的 VF **VFId**所返回的成员[ **NDIS\_NIC\_交换机\_VF\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451593)结构。

    **请注意**  仅过量驱动程序可以获取这种方式中的取景器标识符。

     

通过 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_NIC\_交换机\_VF\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451593)结构。 此结构包含有关指定 VF 配置参数。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID 方法请求的 OID\_NIC\_交换机\_VF\_微型端口驱动程序，并返回以下状态代码的 OID 的 OID 方法请求参数\_NIC\_交换机\_VF\_参数。

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
<td><p>请求已成功完成。 <strong>InformationBuffer</strong>成员将指向<a href="https://msdn.microsoft.com/library/windows/hardware/hh451593" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451593)"> <strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong> </a>结构。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>微型端口驱动程序不支持的单个根 I/O 虚拟化 (SR-IOV) 接口，或未启用要使用的界面。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>一个或多个的成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh451593" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451593)"> <strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度不超过 sizeof (<a href="https://msdn.microsoft.com/library/windows/hardware/hh451593" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451593)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>)。 NDIS 集<strong>数据。METHOD_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 集<strong>数据。METHOD_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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
[**NDIS\_NIC\_SWITCH\_VF\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451593)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_SWITCH\_ENUM\_VFS](oid-nic-switch-enum-vfs.md)

[**NDIS\_NIC\_SWITCH\_VF\_INFO**](https://msdn.microsoft.com/library/windows/hardware/hh451591)

[OID\_NIC\_SWITCH\_VF\_PARAMETERS](oid-nic-switch-vf-parameters.md)

 

 




