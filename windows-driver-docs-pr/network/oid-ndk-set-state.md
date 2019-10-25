---
title: OID_NDK_SET_STATE
description: 作为一个集请求，NDIS 和过量驱动程序使用 OID_NDK_SET_STATE OID 来设置微型端口适配器的 NDK 功能的状态。
ms.assetid: 5BA49F42-FE37-4860-B68F-92A7F4007639
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NDK_SET_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 017e0e4a059b37e0e9b0470366b510ea34af4650
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844105"
---
# <a name="oid_ndk_set_state"></a>OID\_NDK\_集\_状态


作为集请求，NDIS 和过量驱动程序使用 OID\_NDK\_设置\_状态 OID 来设置微型端口适配器的 NDK 功能的状态。

提供 NDK 服务的 NDIS 6.30 和更高版本的微型端口驱动程序必须支持此 OID。 否则，此 OID 是可选的。

<a name="remarks"></a>备注
-------

NDIS 使用[**ndis\_oid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)的**InformationBuffer**成员向此 oid 发出\_请求结构，该请求结构指向等于 sizeof （**布尔值**）的**布尔值**和**InformationBufferLength**成员。

-   如果**布尔**值为**TRUE** ，并且 **\*NetworkDirect**关键字值为非零值，则必须启用微型端口适配器的 NDK 功能。

    微型端口驱动程序可以通过执行以下操作来读取 **\*NetworkDirect**关键字值：

    1.  在初始化微型端口驱动程序时，通过[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)函数返回的 NDIS 句柄调用[**NdisOpenConfigurationEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex) 。 有关调用**NdisOpenConfigurationEx**的详细信息，请参阅[在 NDIS 6.0 微型端口驱动程序中读取注册表](https://docs.microsoft.com/windows-hardware/drivers/network/reading-the-registry-in-an-ndis-6-0-miniport-driver)。

    2.  调用[**NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)，传递：

        -   *关键字*参数的 "\*NetworkDirect"

        -   *ParameterType*参数的**NdisParameterInteger**

-   如果**布尔**值为**FALSE**，则必须禁用微型端口适配器的 NDK 功能。

若要启用或禁用其 NDK 功能，微型端口驱动程序的[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)回调函数应遵循[启用和禁用 NDK 功能](https://docs.microsoft.com/windows-hardware/drivers/network/enabling-and-disabling-ndk-functionality)中的步骤。

**请注意**  支持 NDK 的微型端口驱动程序绝不能从其[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数的上下文中调用[**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent) ，因为这样做可能会导致死锁。 相反，它应从某个其他上下文调用**NdisMNetPnPEvent** ，或将工作项排队。

 

支持 NDK 的微型端口驱动程序的[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数必须返回 OID **\_SUCCESS 的状态**，\_NDK\_设置\_状态 OID 请求，除非发生故障。 驱动程序不得将**NDIS\_状态返回\_挂起状态**。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)

[**NdisQueueIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisqueueioworkitem)

[**NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)

[**NDK\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)

[OID\_NDK\_集\_状态](oid-ndk-set-state.md)

 

 




