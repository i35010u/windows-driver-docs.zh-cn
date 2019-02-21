---
title: OID_NIC_SWITCH_ENUM_SWITCHES
description: 基础驱动程序或用户模式应用程序发出的对象标识符 (OID) 查询请求的 OID_NIC_SWITCH_ENUM_SWITCHES 以获取数组。
ms.assetid: 706C3F1C-239F-4731-A38E-E150D26C79A5
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_ENUM_SWITCHES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 20213059153311ea49056c5b42b8b5f2855dd98e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541814"
---
# <a name="oidnicswitchenumswitches"></a>OID\_NIC\_交换机\_枚举\_开关


基础驱动程序或用户模式应用程序颁发的 OID 的对象标识符 (OID) 查询请求\_NIC\_交换机\_枚举\_交换机以获取数组。 数组中的每个元素指定网络适配器已创建一个 NIC 开关的特性。

通过此 OID 查询请求的成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含指向包含以下各项的缓冲区的指针：

-   [ **NDIS\_NIC\_交换机\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh451584)结构，用于定义数组中元素数。

-   一个数组[ **NDIS\_NIC\_交换机\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451582)结构。 每个这些结构包含有关网络适配器上创建一个 NIC 交换机的信息。

    **请注意**  如果网络适配器不具有任何 NIC 开关，该驱动程序集**NumElements**的成员[ **NDIS\_NIC\_交换机\_INFO\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh451584)为零，并无结构[ **NDIS\_NIC\_交换机\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451582)返回的结构。

     

<a name="remarks"></a>备注
-------

基础驱动程序和用户模式应用程序颁发的 OID 的 OID 查询请求\_NIC\_交换机\_枚举\_交换机，以枚举网络适配器上创建的 NIC 开关。

**请注意**  从 Windows Server 2012 开始，单根 I/O 虚拟化 (SR-IOV) 接口仅支持的默认 NIC 切换上的网络适配器。 因此，返回[ **NDIS\_NIC\_交换机\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh451584)结构必须指定单个[ **NDIS\_NIC\_切换\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451582)元素的引用的 NDIS 的标识符的默认 NIC 交换机\_默认\_交换机\_ID。

 

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID 查询请求的 OID\_NIC\_交换机\_枚举\_开关微型端口驱动程序的请求。 驱动程序将不会颁发此 OID 请求。

NDIS 时处理 OID\_NIC\_交换机\_枚举\_开关请求，它将返回一个下面的状态代码。

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
<td><p>微型端口驱动程序不支持 SR-IOV 接口，或未启用要使用的界面。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>一个或多个的成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh451577" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_INFO_ARRAY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451577)"> <strong>NDIS_NIC_SWITCH_INFO_ARRAY</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 集<strong>数据。QUERY_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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
[**NDIS\_NIC\_交换机\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451582)

[**NDIS\_NIC\_交换机\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh451584)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[OID\_NIC\_SWITCH\_CREATE\_SWITCH](oid-nic-switch-create-switch.md)

[OID\_NIC\_SWITCH\_PARAMETERS](oid-nic-switch-parameters.md)

 

 




