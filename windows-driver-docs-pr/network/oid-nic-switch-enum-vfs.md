---
title: OID_NIC_SWITCH_ENUM_VFS
description: 基础驱动程序或用户模式应用程序发出的对象标识符 (OID) 方法请求的 OID_NIC_SWITCH_ENUM_VFS 以获取数组。
ms.assetid: ABACB70C-9307-4560-93DD-0475AD1FFF10
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_ENUM_VFS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c3ea8f06739035dac11b7325a714b01255176dc8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359269"
---
# <a name="oidnicswitchenumvfs"></a>OID\_NIC\_SWITCH\_ENUM\_VFS


基础驱动程序或用户模式应用程序颁发的 OID 的对象标识符 (OID) 方法请求\_NIC\_交换机\_枚举\_VFS 以获取数组。 数组中的每个元素指定的属性的 PCI Express (PCIe) 虚拟函数 (VF) 附加到 NIC 的网络适配器的 NIC 交换机上切换。

通过此 OID 查询请求的成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含指向包含以下各项的缓冲区的指针：

-   [ **NDIS\_NIC\_交换机\_VF\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh451592)结构，用于定义数组中元素数。

-   一个数组[ **NDIS\_NIC\_交换机\_VF\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451591)结构。 包含有关单个 VF NIC 交换机上的网络适配器的信息，以及每个这些结构。 取景器附加到通过 OID 方法请求的 NIC 交换机[OID\_NIC\_切换\_分配\_VF](oid-nic-switch-allocate-vf.md)。

    **请注意**  如果没有 VFs 已附加到网络适配器上的 NIC 交换机**NumElements**的成员[ **NDIS\_NIC\_交换机\_VF\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh451592)结构设置为零并且没有[ **NDIS\_NIC\_开关\_VF\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/hh451591)返回结构。

     

<a name="remarks"></a>备注
-------

基础驱动程序和用户模式应用程序颁发的 OID 的 OID 方法请求\_NIC\_切换\_枚举\_VFS 枚举 VFs 连接到网络适配器的 NIC 交换机。

驱动程序或应用程序发出 OID 请求之前，必须将格式化[ **NDIS\_NIC\_交换机\_VF\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh451592)随请求一起传递的结构。 驱动程序或应用程序初始化时，必须遵循这些准则**NDIS\_NIC\_交换机\_VF\_信息\_数组**结构：

-   如果 NDIS\_NIC\_交换机\_VF\_信息\_数组\_枚举\_ON\_特定\_中设置了开关标志**标志**成员、 驱动程序或应用程序必须设置**SwitchId** SR-IOV 网络适配器上的 NIC 交换机标识符的成员。 通过以这种方式设置这些成员，仅对指定的 NIC 的 SR-IOV 网络适配器上切换，则返回 VF 信息。

    **请注意**  过量的驱动程序和用户模式应用程序可以通过发出的 OID 查询请求获取 NIC 交换机标识符[OID\_NIC\_切换\_枚举\_开关](oid-nic-switch-enum-switches.md)。

     

-   如果**标志**成员设置为零，则驱动程序或应用程序必须设置**SwitchId**为零的成员。 通过以这种方式设置这些成员，返回 VF 信息为所有 NIC 切换 SR-IOV 网络适配器上。

**请注意**  从 Windows Server 2012 开始，Windows 上的网络适配器支持仅默认 NIC 切换。 无论中设置的标志**标志**成员**SwitchId**成员必须设置为 NDIS\_默认\_开关\_id。

 

有关 NIC 开关的详细信息，请参阅[NIC 开关](https://msdn.microsoft.com/library/windows/hardware/hh439961)。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID 方法请求的 OID\_NIC\_交换机\_枚举\_VFS 微型端口驱动程序的请求。 驱动程序将不会颁发此 OID 请求。

NDIS 时处理 OID\_NIC\_交换机\_枚举\_VFS 请求，它将返回一个下面的状态代码。

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
<td><p>一个或多个的成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh451592" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_INFO_ARRAY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451592)"> <strong>NDIS_NIC_SWITCH_VF_INFO_ARRAY</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 集<strong>数据。METHOD_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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
[**NDIS\_NIC\_SWITCH\_VF\_INFO**](https://msdn.microsoft.com/library/windows/hardware/hh451591)

[**NDIS\_NIC\_SWITCH\_VF\_INFO\_ARRAY**](https://msdn.microsoft.com/library/windows/hardware/hh451592)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_SWITCH\_CREATE\_SWITCH](oid-nic-switch-create-switch.md)

[OID\_NIC\_SWITCH\_VF\_PARAMETERS](oid-nic-switch-vf-parameters.md)

 

 




