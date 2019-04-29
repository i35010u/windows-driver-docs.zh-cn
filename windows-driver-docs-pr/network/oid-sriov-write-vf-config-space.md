---
title: OID_SRIOV_WRITE_VF_CONFIG_SPACE
description: 基础驱动程序发出的对象标识符 (OID) 组请求的 OID_SRIOV_WRITE_VF_CONFIG_SPACE 将数据写入到的 PCI Express (PCIe) 配置空间的指定 PCIe 虚拟函数 (VF) 上的网络适配器。
ms.assetid: 0D9866A6-A8C6-4B0A-8D17-A632E1AE37BF
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_WRITE_VF_CONFIG_SPACE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f8adaaef91ea9e86187a83cbb7fdabd249490845
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351333"
---
# <a name="oidsriovwritevfconfigspace"></a>OID\_SRIOV\_编写\_VF\_配置\_空间


基础驱动程序将发出对象标识符 (OID) 组请求的 OID\_SRIOV\_编写\_VF\_配置\_空间来写入数据的指定 PCIe PCI Express (PCIe) 配置空间虚拟函数 (VF) 上的网络适配器。

基础驱动程序此 OID 集向发出请求的微型端口驱动程序的网络适配器的 PCIe 物理函数 (PF)。 此 OID 方法请求是必需的支持的单个根 I/O 虚拟化 (SR-IOV) 接口的 PF 微型端口驱动程序。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含调用方分配的缓冲区的指针。 此缓冲区已格式化为包含以下信息：

-   [ **NDIS\_SRIOV\_编写\_VF\_配置\_空间\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451688)结构，其中包含VF PCI 配置空间的写入操作的参数。

-   包含要写入到 PCI 配置空间的数据的附加缓冲区空间。

<a name="remarks"></a>备注
-------

VF 微型端口驱动程序在运行 HYPER-V 子分区的来宾操作系统中。 正因为如此，VF 微型端口驱动程序不能直接访问硬件资源，例如 VF PCI 配置空间。 只有 PF 微型端口驱动程序，它运行在管理操作系统的 HYPER-V 父分区中，可访问以 VF PCI 配置空间。

基础驱动程序，如虚拟化堆栈中，发出 OID 集请求的 OID\_SRIOV\_编写\_VF\_CONFIG\_空间 VF 微型端口驱动程序调用时[ **NdisMSetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff563670)要写入到其 PCI 配置空间。

当它处理 OID 方法请求的 OID\_SRIOV\_编写\_VF\_配置\_空间，PF 微型端口驱动程序必须遵循这些准则：

-   PF 微型端口驱动程序必须验证指定 VF **VFId**的成员[ **NDIS\_SRIOV\_编写\_VF\_配置\_空间\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451688)结构，具有先前已分配的资源。 PF 微型端口驱动程序分配资源，用于通过 OID 方法请求的 VF [OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)。

    如果尚未分配指定 VF 的资源的驱动程序必须失败 OID 请求。

-   PF 微型端口驱动程序调用[ **NdisMSetVirtualFunctionBusData** ](https://msdn.microsoft.com/library/windows/hardware/hh451526)要写入到请求的 PCI 配置空间。 但是，PF 微型端口驱动程序还可以返回驱动程序已从以前缓存的 VF PCI 配置空间数据读取或写入操作的 PCI 配置空间。

    **请注意**  如果的独立硬件供应商 (IHV) 提供虚拟总线驱动程序 (VBD) 作为其 SR-IOV 的一部分[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)，不能调用其 PF 微型端口驱动程序[ **NdisMSetVirtualFunctionBusData**](https://msdn.microsoft.com/library/windows/hardware/hh451526)。 相反，该驱动程序必须与通过专用通信通道，VBD 接口，并请求，调用 VBD [ *SetVirtualFunctionData*](https://msdn.microsoft.com/library/windows/hardware/hh451552)。 此函数从其公开[GUID\_VPCI\_界面\_标准](https://msdn.microsoft.com/library/windows/hardware/hh451146)基础的虚拟 PCI (VPCI) 总线驱动程序支持的接口。

     

如果 PF 微型端口驱动程序才能成功完成 OID 请求，该驱动程序必须请求的 PCI 配置空间数据复制到引用的缓冲区**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构。 该驱动程序将数据复制到指定的偏移量处的缓冲区**BufferOffset**的成员[ **NDIS\_SRIOV\_读取\_VF\_配置\_空间\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451681)结构。

有关详细信息，请参阅[设置的虚拟函数的 PCI 配置数据](https://msdn.microsoft.com/library/windows/hardware/hh440229)。

### <a name="return-status-codes"></a>返回状态代码

PF 微型端口驱动程序返回以下状态代码之一 OID 设置请求的 OID\_SRIOV\_编写\_VF\_配置\_空间。

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
<td><p>PF 微型端口驱动程序不支持的单个根 I/O 虚拟化 (SR-IOV) 接口，或未启用要使用的界面。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>一个或多个的成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh451688" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_WRITE_VF_CONFIG_SPACE_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451688)"> <strong>NDIS_SRIOV_WRITE_VF_CONFIG_SPACE_PARAMETERS</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 集<strong>数据。SET_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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
[GUID\_VPCI\_INTERFACE\_STANDARD](https://msdn.microsoft.com/library/windows/hardware/hh451146)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SRIOV\_编写\_VF\_CONFIG\_空间\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451688)

[**NdisMSetBusData**](https://msdn.microsoft.com/library/windows/hardware/ff563670)

[**NdisMSetVirtualFunctionBusData**](https://msdn.microsoft.com/library/windows/hardware/hh451526)

[OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_SRIOV\_读取\_VF\_配置\_空间](oid-sriov-read-vf-config-space.md)

[*SetVirtualFunctionData*](https://msdn.microsoft.com/library/windows/hardware/hh451552)

 

 




