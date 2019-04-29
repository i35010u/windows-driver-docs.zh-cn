---
title: OID_NIC_SWITCH_CREATE_SWITCH
description: NDIS 发出一个对象标识符 (OID) 方法请求 OID_NIC_SWITCH_CREATE_SWITCH 的网络适配器上创建一个 NIC 开关。
ms.assetid: 16FFC6A4-11A6-45A1-ABCF-8C1EBE3FD953
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_CREATE_SWITCH 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 939517cb5a6517e793cbe924ebb6fb7a246386e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383603"
---
# <a name="oidnicswitchcreateswitch"></a>OID\_NIC\_交换机\_创建\_开关


NDIS 发出对象标识符 (OID) 方法请求的 OID\_NIC\_切换\_创建\_网络适配器上切换开关来创建一个 NIC。 它处理此 OID 请求，微型端口驱动程序会为该适配器上的 NIC 开关分配资源。

NDIS 微型端口驱动程序的网络适配器的 PCI Express (PCIe) 物理函数 (PF) 向发出此 OID 方法请求。 此 OID 方法请求是必需的支持的单个根 I/O 虚拟化 (SR-IOV) 接口的 PF 微型端口驱动程序。

**请注意**  过量驱动程序，例如协议或筛选器驱动程序不能发出 OID 方法请求的 OID\_NIC\_交换机\_创建\_切换到 PF 微型端口驱动程序。

 

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_NIC\_交换机\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451587)结构。

<a name="remarks"></a>备注
-------

当它收到 OID 方法请求的 OID\_NIC\_交换机\_创建\_开关，PF 微型端口驱动程序必须执行以下操作：

1.  如果 PF 微型端口驱动程序支持静态交换机创建和配置，它创建 NIC 开关，当调用 NDIS [ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)。 当驱动程序处理此 OID 请求时，它必须验证中的配置参数[ **NDIS\_NIC\_交换机\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451587)结构。 参数必须与使用的驱动程序以在调用期间创建的交换机相同*MiniportInitializeEx*。 如果不为 true，则驱动程序必须失败 OID 请求。

    有关详细信息，请参阅[静态创建的 NIC 交换机](https://msdn.microsoft.com/library/windows/hardware/hh440256)。

2.  如果 PF 微型端口驱动程序支持动态交换机创建和配置，该驱动程序必须验证的配置值[ **NDIS\_NIC\_切换\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451587)结构并创建 NIC 交换机基于这些值。

    有关详细信息，请参阅[动态创建的 NIC 交换机](https://msdn.microsoft.com/library/windows/hardware/hh406694)。

3.  PF 微型端口驱动程序必须为 NIC 交换机上的默认 VPort 分配所需的硬件和软件资源。

    **请注意**  VPort 始终通过 OID 的 OID 请求创建的默认值\_NIC\_交换机\_创建\_开关，通过的 OID 请求删除[OID\_NIC\_交换机\_删除\_交换机](oid-nic-switch-delete-switch.md)。 OID 请求[OID\_NIC\_交换机\_创建\_VPORT](oid-nic-switch-create-vport.md)并[OID\_NIC\_交换机\_删除\_VPORT](oid-nic-switch-delete-vport.md)用于创建和删除 NIC 交换机上的非默认 VPorts。

     

4.  支持动态交换机创建和配置 PF 微型端口驱动程序必须通过调用启用 SR-IOV 交换机上的虚拟化[ **NdisMEnableVirtualization**](https://msdn.microsoft.com/library/windows/hardware/hh451481)。 此调用将配置**NumVFs**成员和**VF 启用**位中的 SR-IOV 扩展功能的适配器的 PCI Express (PCIe) 配置空间。

    有关 SR-IOV 配置空间的详细信息，请参阅 PCI SIG[单根 I/O 虚拟化和共享 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742)规范。

    **请注意**  如果 PF 微型端口驱动程序支持静态交换机创建，它将启用 SR-IOV 虚拟化后创建开关时[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)称为.

     

如果 PF 微型端口驱动程序已成功完成时 OID 方法请求的 OID\_NIC\_交换机\_创建\_开关，它允许发生以下情况：

-   可以分配 VFs 通过 OID 方法请求的 NIC 交换机上[OID\_NIC\_切换\_分配\_VF](oid-nic-switch-allocate-vf.md)。

-   可以创建非默认 VPorts 通过 OID 方法请求的 NIC 交换机上[OID\_NIC\_切换\_创建\_VPORT](oid-nic-switch-create-vport.md)。

有关如何处理此 OID 请求的详细信息，请参阅[处理 OID\_NIC\_交换机\_创建\_切换请求](https://msdn.microsoft.com/library/windows/hardware/hh451370)。

### <a name="return-status-codes"></a>返回状态代码

PF 微型端口驱动程序将返回一个 OID 的 OID 方法请求的以下状态代码\_NIC\_交换机\_创建\_开关。

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
<td><p>一个或多个的成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh451587" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451587)"> <strong>NDIS_NIC_SWITCH_PARAMETERS</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度不超过 sizeof (<a href="https://msdn.microsoft.com/library/windows/hardware/hh451587" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451587)"><strong>NDIS_NIC_SWITCH_PARAMETERS</strong></a>)。 PF 微型端口驱动程序必须设置<strong>数据。METHOD_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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
[*MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_NIC\_SWITCH\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451587)

[**NdisMEnableVirtualization**](https://msdn.microsoft.com/library/windows/hardware/hh451481)

[OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_SWITCH\_CREATE\_VPORT](oid-nic-switch-create-vport.md)

 

 




