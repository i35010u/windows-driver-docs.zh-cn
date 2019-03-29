---
title: OID_SRIOV_PF_LUID
description: 基础驱动程序发出的对象标识符 (OID) 查询请求的 OID_SRIOV_PF_LUID 接收与 PCI Express (PCIe) 物理函数 (PF) 的网络适配器关联的本地唯一标识符 (LUID)。
ms.assetid: 363D308D-CE88-4F3B-81FF-37A2D86CB7BC
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_PF_LUID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 65992a7e5f8afe66bf48954040c9b882acab7169
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575810"
---
# <a name="oidsriovpfluid"></a>OID\_SRIOV\_PF\_LUID


基础驱动程序将发出对象标识符 (OID) 查询请求的 OID\_SRIOV\_PF\_LUID 接收关联与 PCI Express (PCIe) 物理函数 (PF) 的网络的本地唯一标识符 (LUID)适配器。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_SRIOV\_PF\_LUID\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451678)结构。

<a name="remarks"></a>备注
-------

NDIS 为 NDIS 调用之前 PF 生成 LUID [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389) PF.的微型端口驱动程序的函数 此 LUID 之前 NDIS 调用都有效[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)驱动程序的函数。

**请注意**  的值**Luid**成员不同于**NetLuid**隶属[ **NDIS\_微型端口\_INIT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565972)结构。 此结构传递给微型端口驱动程序通过*MiniportInitParameters*的参数[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)。

 

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID 查询请求的 OID\_SRIOV\_PF\_LUID 微型端口驱动程序的请求。 驱动程序将不会颁发此 OID 请求。

NDIS 时处理 OID\_SRIOV\_PF\_LUID 请求，它将返回一个下面的状态代码。

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

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SRIOV\_PF\_LUID\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451678)

 

 




