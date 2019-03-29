---
title: OID_QOS_PARAMETERS
description: 数据中心桥接 (DCB) 组件 (Msdcb.sys) 发出一个对象标识符 (OID) 方法请求 OID_QOS_PARAMETERS 的网络适配器上配置本地 NDIS 服务质量 (QoS) 参数。
ms.assetid: 1CA97C8A-8F5B-4AB2-B68E-DF1FA772C08F
ms.date: 08/08/2017
keywords: -OID_QOS_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 26d72a6148c7e5c1ad8f55b9b8d1ecc8f7fd0455
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568230"
---
# <a name="oidqosparameters"></a>OID\_QOS\_参数


数据中心桥接 (DCB) 组件 (Msdcb.sys) 颁发的 OID 的对象标识符 (OID) 方法请求\_QOS\_要网络适配器上配置本地 NDIS 服务质量 (QoS) 参数的参数。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构。

**请注意**此 OID 方法请求是必需的 NDIS QoS 支持 IEEE 802.1 数据中心桥接 (DCB) 接口的微型端口驱动程序。



<a name="remarks"></a>备注
-------

微型端口驱动程序获取 OID 的 OID 方法请求通过本地的 NDIS QoS 参数\_QOS\_参数。 这些参数定义的网络适配器确定传输，优先级的方式或*出口*，数据包。 有关这些参数的详细信息，请参阅[NDIS QoS 参数的概述](https://msdn.microsoft.com/library/windows/hardware/hh440130)。

**请注意**DCB 组件可以发出 OID 方法请求的 OID 仅\_QOS\_参数。 基础协议或筛选器驱动程序必须发出此 OID。 有关 DCB 组件的详细信息，请参阅[NDIS QoS 体系结构的数据中心桥接](https://msdn.microsoft.com/library/windows/hardware/hh451627)。



DCB 组件发出 OID\_QOS\_参数请求在以下情况下：

-   系统管理员安装或卸载 Microsoft DCB 服务器功能。

    有关 DCB 服务器功能的详细信息，请参阅[系统提供 DCB 组件](https://msdn.microsoft.com/library/windows/hardware/hh440259)。

-   系统管理员启用或禁用 DCB 服务器功能，尽管仍然安装该功能。

-   系统管理员更改任何 DCB 服务器功能参数。

-   操作系统启动或重新启动时安装 DCB 服务器功能。

微型端口驱动程序时处理 OID 方法请求的 OID\_QOS\_参数，它必须遵循以下准则：

-   微型端口驱动程序将在数据复制[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)到其缓存本地 NDIS QoS 参数的结构。 该驱动程序然后将解析其操作的 NDIS QoS 参数基于本地的 NDIS QoS 参数其缓存和其缓存它来自远程对等方的 NDIS QoS 参数。

    有关如何微型端口驱动程序解决其操作的参数的详细信息，请参阅[解析操作的 NDIS QoS 参数](https://msdn.microsoft.com/library/windows/hardware/hh440220)。

-   微型端口驱动程序必须修改包含在任何数据[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构。 该驱动程序必须完成 OID 方法请求，并将原始数据中的返回**NDIS\_QOS\_参数**结构。

-   **NDIS\_QOS\_参数\_WILLING**标志指定是否微型端口驱动程序启用或禁用本地数据中心桥接交换 (DCBX) 愿意状态。 驱动程序处理此标志，如下所示：

    -   如果设置此标志，微型端口驱动程序必须启用本地 DCBX 愿意状态。 这将允许驱动程序进行远程配置 QoS 设置。 在这种情况下，该驱动程序解析其操作的 QoS 参数基于远程 QoS 参数。 微型端口驱动程序也可以解决基于由独立硬件供应商 (IHV) 定义的任何专有 QoS 设置其操作的 QoS 参数。

    -   如果未设置此标志，微型端口驱动程序必须禁用本地 DCBX 愿意状态。 这将允许驱动程序解析其操作的 QoS 参数从其本地 QoS 参数而不是远程的 QoS 参数。 微型端口驱动程序还必须禁用或为其重写任何本地 QoS 参数的相关**NDIS\_QOS\_参数\_*Xxx*\_配置**未设置标志。

        例如，微型端口驱动程序可以重写由 IHV 定义的 QoS 参数其专有设置是未配置本地 QoS 参数。 如果未使用指定的本地 QoS 参数没有专有设置**NDIS\_QOS\_参数\_*Xxx*\_配置**标志，该驱动程序必须禁用这些网络适配器上的 QoS 参数。

        **请注意**驱动程序还可以重写配置的本地 QoS 参数如果他们要入侵使用协议或技术的网络适配器启用的 QoS 参数。 例如，如果通过 Ethernet (FCoE) 协议情况下，启用通过光纤通道的远程启动的网络适配器驱动程序可以重写本地 QoS 参数。

    有关本地 DCBX 愿意状态，请参阅[管理本地 DCBX 愿意状态](https://msdn.microsoft.com/library/windows/hardware/hh706282)。

有关如何将微型端口驱动程序覆盖本地 QoS 参数的详细信息，请参阅[管理的 NDIS QoS 参数](https://msdn.microsoft.com/library/windows/hardware/hh464015)。

**请注意**重写本地 QoS 参数不应导致微型端口驱动程序故障 OID 方法请求的 OID\_QOS\_参数。

有关如何微型端口驱动程序管理的本地 QoS 参数的详细信息，请参阅[设置本地 NDIS QoS 参数](https://msdn.microsoft.com/library/windows/hardware/hh440225)。

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序返回以下状态代码之一。

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
<td><p>NDIS_STATUS_PENDING</p></td>
<td><p>OID 请求正在等待完成。 当微型端口驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff563622" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563622)"> <strong>NdisMOidRequestComplete</strong></a>、 NDIS 将传递的最后一个状态代码和结果与 OID 请求完成处理程序的调用方在请求后完成。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>微型端口驱动程序不支持的 NDIS QoS 接口。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>一个或多个成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh451640" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451640)"> <strong>NDIS_QOS_PARAMETERS</strong> </a>结构包含不正确的值。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区长度小于<strong>sizeof</strong>(<a href="https://msdn.microsoft.com/library/windows/hardware/hh451640" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451640)"><strong>NDIS_QOS_PARAMETERS</strong></a>)。 NDIS 集<strong>数据。QUERY_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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
[**NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_QOS\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)

[**NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)

[**NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)








