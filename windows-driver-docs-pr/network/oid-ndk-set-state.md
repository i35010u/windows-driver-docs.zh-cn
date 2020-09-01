---
title: OID_NDK_SET_STATE
description: 作为一个集请求，NDIS 和过量驱动程序使用 OID_NDK_SET_STATE OID 来设置微型端口适配器的 NDK 功能的状态。
ms.assetid: 5BA49F42-FE37-4860-B68F-92A7F4007639
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NDK_SET_STATE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 72f4542e24934d9e756670e970056b7d6b5923f9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216604"
---
# <a name="oid_ndk_set_state"></a>OID \_ NDK \_ 集 \_ 状态


作为一个集请求，NDIS 和过量驱动程序使用 OID \_ NDK \_ 集 \_ 状态 OID 来设置微型端口适配器的 NDK 功能的状态。

提供 NDK 服务的 NDIS 6.30 和更高版本的微型端口驱动程序必须支持此 OID。 否则，此 OID 是可选的。

<a name="remarks"></a>备注
-------

NDIS 用指向**布尔值**和**InformationBufferLength**成员（等于 sizeof (**布尔**) ）的[**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员颁发此 OID。

-   如果**布尔**值为**TRUE** ，并且** \* NetworkDirect**关键字值为非零，则必须启用微型端口适配器的 NDK 功能。

    微型端口驱动程序可以通过执行以下操作来读取** \* NetworkDirect**关键字值：

    1.  在初始化微型端口驱动程序时，通过[**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)函数返回的 NDIS 句柄调用[**NdisOpenConfigurationEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex) 。 有关调用 **NdisOpenConfigurationEx**的详细信息，请参阅 [在 NDIS 6.0 微型端口驱动程序中读取注册表](/previous-versions/windows/hardware/network/reading-the-registry-in-an-ndis-6-0-miniport-driver)。

    2.  调用 [**NdisReadConfiguration**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)，传递：

        -   \**关键字*参数的 "NetworkDirect"

        -   *ParameterType*参数的**NdisParameterInteger**

-   如果 **布尔** 值为 **FALSE**，则必须禁用微型端口适配器的 NDK 功能。

若要启用或禁用其 NDK 功能，微型端口驱动程序的 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 回调函数应遵循 [启用和禁用 NDK 功能](./enabling-and-disabling-ndk-functionality.md)中的步骤。

**注意**   支持 NDK 的微型端口驱动程序绝不能从其[*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数的上下文中调用[**NdisMNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent) ，因为这样做可能会导致死锁。 相反，它应从某个其他上下文调用 **NdisMNetPnPEvent** ，或将工作项排队。

 

除非出现错误，否则支持 NDK 的微型端口驱动程序的 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数必须返回 OID NDK ** \_ ** \_ \_ 集 \_ 状态 oid 请求的状态 "成功"。 驱动程序不得返回 **NDIS \_ 状态 " \_ 挂起**"。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>无受支持的版本</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NdisMNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)

[**NdisQueueIoWorkItem**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisqueueioworkitem)

[**NdisReadConfiguration**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)

[**NDK \_ 适配器**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)

[OID \_ NDK \_ 集 \_ 状态](oid-ndk-set-state.md)

 

