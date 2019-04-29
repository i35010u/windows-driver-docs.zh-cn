---
title: OID_NDK_SET_STATE
description: 作为 set 请求，NDIS 和基础驱动程序使用 OID_NDK_SET_STATE OID 来设置 NDK 微型端口适配器的功能的状态。
ms.assetid: 5BA49F42-FE37-4860-B68F-92A7F4007639
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NDK_SET_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d8fe2aad2183e158d6f04865357cee9abe3938a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391650"
---
# <a name="oidndksetstate"></a>OID\_NDK\_SET\_STATE


为 set 请求，NDIS 和基础驱动程序使用 OID\_NDK\_设置\_状态 OID 的微型端口适配器的 NDK 功能将状态设置。

NDIS 6.30 和更高版本的微型端口驱动程序提供 NDK 服务必须支持此 OID。 否则，此 OID 是可选的。

<a name="remarks"></a>备注
-------

NDIS 发出具有此 OID **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构指向**布尔**并**InformationBufferLength**成员等于 sizeof (**布尔**)。

-   如果**布尔**值是**TRUE**并 **\*NetworkDirect**关键字值不为零，必须启用 NDK 微型端口适配器的功能。

    微型端口驱动程序可以读取 **\*NetworkDirect**关键字值，通过执行以下操作：

    1.  调用[ **NdisOpenConfigurationEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563717)与的 NDIS 处理[ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)函数时返回微型端口驱动程序已初始化。 有关调用详细信息**NdisOpenConfigurationEx**，请参阅[读取的注册表中 NDIS 6.0 微型端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff570429)。

    2.  调用[ **NdisReadConfiguration**](https://msdn.microsoft.com/library/windows/hardware/ff564511)，并传递：

        -   "\*NetworkDirect"有关*关键字*参数

        -   **NdisParameterInteger**有关*ParameterType*参数

-   如果**布尔**值是**FALSE**，必须禁用 NDK 微型端口适配器的功能。

若要启用或禁用其 NDK 功能，微型端口驱动程序的[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)回调函数应按照中的步骤[启用和禁用 NDK 功能](https://msdn.microsoft.com/library/windows/hardware/dn163547).

**请注意**  永远不会调用 NDK 支持的微型端口驱动程序必须[ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)的上下文从其[ *MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416)函数，因为这样做可能导致死锁。 相反，它应调用**NdisMNetPnPEvent**从一些其他上下文或队列工作项。

 

NDK 支持的微型端口驱动程序的[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)函数必须返回**状态\_成功**oid\_NDK\_设置\_状态 OID 请求，除非发生故障。 该驱动程序不能返回**NDIS\_状态\_PENDING**。

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


[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NdisMNetPnPEvent**](https://msdn.microsoft.com/library/windows/hardware/ff563616)

[**NdisQueueIoWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff563775)

[**NdisReadConfiguration**](https://msdn.microsoft.com/library/windows/hardware/ff564511)

[**NDK\_ADAPTER**](https://msdn.microsoft.com/library/windows/hardware/hh439848)

[OID\_NDK\_设置\_状态](oid-ndk-set-state.md)

 

 




