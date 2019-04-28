---
title: OID_SRIOV_CURRENT_CAPABILITIES
description: 基础驱动程序发出的对象标识符 (OID) 查询请求的 OID_SRIOV_CURRENT_CAPABILITIES 以获取当前的单个根 I/O 虚拟化 (SR-IOV) 功能的网络适配器。
ms.assetid: EE76B3F8-2883-484A-B2EE-6F7D4738934E
ms.date: 08/08/2017
keywords: -OID_SRIOV_CURRENT_CAPABILITIES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e4bad1cad357e8a0587216b301b4df31bb9c7209
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351302"
---
# <a name="oidsriovcurrentcapabilities"></a>OID\_SRIOV\_当前\_功能


基础驱动程序将发出对象标识符 (OID) 查询请求的 OID\_SRIOV\_当前\_功能，以获取当前的单根 I/O 虚拟化 (SR-IOV) 功能的网络适配器。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_SRIOV\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451677)结构。

<a name="remarks"></a>备注
-------

从开始 NDIS 6.30，微型端口驱动程序提供的网络适配器上启用的 SR-IOV 硬件功能时其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)调用函数。 该驱动程序初始化[ **NDIS\_SRIOV\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451677)结构的当前已启用 SR-IOV 硬件功能和设置**CurrentSriovCapabilities**的成员[ **NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)指向的结构**NDIS\_SRIOV\_功能**结构。 然后调用微型端口驱动程序[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数和集*MiniportAttributes*参数指向的**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**结构。

基础协议和筛选器驱动程序无需发出 OID 查询请求的 OID\_SRIOV\_当前\_功能。 NDIS 按以下方式提供这些驱动程序的网络适配器的当前已启用的 SR-IOV 功能：

-   NDIS 报告到过量协议中的驱动程序的基础网络适配器的当前已启用的 SR-IOV 功能**SriovCapabilities**的成员[ **NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)绑定操作过程中的结构。

-   NDIS 报告到过量中的筛选器驱动程序的基础网络适配器的当前已启用的 SR-IOV 功能**SriovCapabilities**的成员[ **NDIS\_筛选器\_ATTACH\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565481)在附加操作期间的结构。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID 查询请求的 OID\_SRIOV\_当前\_微型端口驱动程序的功能请求。 驱动程序将不会颁发此 OID 请求。

NDIS 时处理 OID\_SRIOV\_当前\_功能请求，它将返回以下状态代码之一：

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
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 微型端口驱动程序必须设置<strong>数据。QUERY_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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
[**NDIS\_BIND\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff564832)

[**NDIS\_FILTER\_ATTACH\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff565481)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)

[**NDIS\_SRIOV\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451677)

[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)

 

 




