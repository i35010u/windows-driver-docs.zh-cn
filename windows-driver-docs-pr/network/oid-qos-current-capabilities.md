---
title: OID_QOS_CURRENT_CAPABILITIES
description: 基础驱动程序发出的对象标识符 (OID) 查询请求的 OID_QOS_CURRENT_CAPABILITIES 以获取当前已启用的 NDIS 服务质量 (QoS) 硬件功能的网络适配器。
ms.assetid: E9013EB2-5EDB-4BCB-BC1D-17345B85D1C4
ms.date: 08/08/2017
keywords: -OID_QOS_CURRENT_CAPABILITIES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d876cd65e16c950b0aa64742c94d686d542478b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561505"
---
# <a name="oidqoscurrentcapabilities"></a>OID\_QOS\_当前\_功能


基础驱动程序将发出对象标识符 (OID) 查询请求的 OID\_QOS\_当前\_功能，以获取当前已启用的 NDIS 服务质量 (QoS) 硬件功能的网络适配器。

从 OID 查询请求，成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_QOS\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)结构。

**请注意**  的微型端口驱动程序，支持 IEEE 802.1 数据中心桥接 (DCB) 接口由 NDIS 处理此 OID 查询请求。

 

<a name="remarks"></a>备注
-------

微型端口驱动程序注册的网络适配器的当前已启用 NDIS QoS 硬件功能时其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)调用函数。 驱动程序通过执行以下步骤来注册这些功能：

1.  该驱动程序初始化[ **NDIS\_QOS\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)与启用了 QoS 硬件功能的结构。

2.  驱动程序集**CurrentQosCapabilities**的成员[ **NDIS\_微型端口\_适配器\_硬件\_帮助\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)指向的结构[ **NDIS\_QOS\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)结构。

3.  然后调用微型端口驱动程序[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数和集*MiniportAttributes*参数指向的[ **NDIS\_微型端口\_适配器\_硬件\_帮助\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)结构。

**请注意**  NDIS 不会报告的当前已启用 NDIS QoS 硬件功能的网络适配器在绑定期间过量协议和筛选器驱动程序或附加操作。

 

有关如何注册的 NDIS QoS 功能的详细信息，请参阅[注册的 NDIS QoS 功能](https://msdn.microsoft.com/library/windows/hardware/hh440188)。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID 查询请求的 OID\_QOS\_当前\_微型端口驱动程序，并返回一个的以下状态代码的功能请求。

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
<td><p>微型端口驱动程序不支持的 NDIS QoS 接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度不超过 sizeof (<a href="https://msdn.microsoft.com/library/windows/hardware/hh451629" data-raw-source="[&lt;strong&gt;NDIS_QOS_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451629)"><strong>NDIS_QOS_CAPABILITIES</strong></a>)。 NDIS 集<strong>数据。QUERY_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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
<td><p>版本</p></td>
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

[**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)

[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_QOS\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)

 

 




