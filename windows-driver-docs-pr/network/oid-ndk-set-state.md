---
title: OID_NDK_SET_STATE
description: 作为 set 请求，NDIS 和基础驱动程序使用 OID_NDK_SET_STATE OID 来设置 NDK 微型端口适配器的功能的状态。
ms.assetid: 5BA49F42-FE37-4860-B68F-92A7F4007639
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NDK_SET_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5bc4521807299d4b7573821208341920cdd6b32b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371808"
---
# <a name="oidndksetstate"></a>OID\_NDK\_SET\_STATE


为 set 请求，NDIS 和基础驱动程序使用 OID\_NDK\_设置\_状态 OID 的微型端口适配器的 NDK 功能将状态设置。

NDIS 6.30 和更高版本的微型端口驱动程序提供 NDK 服务必须支持此 OID。 否则，此 OID 是可选的。

<a name="remarks"></a>备注
-------

NDIS 发出具有此 OID **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构指向**布尔**并**InformationBufferLength**成员等于 sizeof (**布尔**)。

-   如果**布尔**值是**TRUE**并 **\*NetworkDirect**关键字值不为零，必须启用 NDK 微型端口适配器的功能。

    微型端口驱动程序可以读取 **\*NetworkDirect**关键字值，通过执行以下操作：

    1.  调用[ **NdisOpenConfigurationEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenconfigurationex)与的 NDIS 处理[ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)函数时返回微型端口驱动程序已初始化。 有关调用详细信息**NdisOpenConfigurationEx**，请参阅[读取的注册表中 NDIS 6.0 微型端口驱动程序](https://docs.microsoft.com/windows-hardware/drivers/network/reading-the-registry-in-an-ndis-6-0-miniport-driver)。

    2.  调用[ **NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreadconfiguration)，并传递：

        -   "\*NetworkDirect"有关*关键字*参数

        -   **NdisParameterInteger**有关*ParameterType*参数

-   如果**布尔**值是**FALSE**，必须禁用 NDK 微型端口适配器的功能。

若要启用或禁用其 NDK 功能，微型端口驱动程序的[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)回调函数应按照中的步骤[启用和禁用 NDK 功能](https://docs.microsoft.com/windows-hardware/drivers/network/enabling-and-disabling-ndk-functionality).

**请注意**  永远不会调用 NDK 支持的微型端口驱动程序必须[ **NdisMNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismnetpnpevent)的上下文从其[ *MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数，因为这样做可能导致死锁。 相反，它应调用**NdisMNetPnPEvent**从一些其他上下文或队列工作项。

 

NDK 支持的微型端口驱动程序的[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数必须返回**状态\_成功**oid\_NDK\_设置\_状态 OID 请求，除非发生故障。 该驱动程序不能返回**NDIS\_状态\_PENDING**。

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


[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismnetpnpevent)

[**NdisQueueIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisqueueioworkitem)

[**NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreadconfiguration)

[**NDK\_ADAPTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_adapter)

[OID\_NDK\_设置\_状态](oid-ndk-set-state.md)

 

 




