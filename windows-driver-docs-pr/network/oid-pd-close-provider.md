---
title: OID_PD_CLOSE_PROVIDER
description: NDIS 协议或筛选器驱动程序将 OID_PD_CLOSE_PROVIDER 的对象标识符（OID）方法请求发送到 PDPI 提供程序，以在 PDPI 提供程序对象中对 PD 功能提供访问权限。
ms.assetid: 8A504A81-6DC8-415C-9FDC-F03657A0EB87
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PD_CLOSE_PROVIDER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a4febedd19324fa449ca53630aaa9b8da0d8a0e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844070"
---
# <a name="oid_pd_close_provider"></a>OID\_PD\_关闭\_提供程序


NDIS 协议或筛选器驱动程序将 OID\_PD\_关闭\_提供程序的对象标识符（OID）方法请求发送到 PDPI 提供程序，以在 PDPI 提供程序对象中提供对 PD 功能的访问权限。

当 NDIS 协议或筛选器驱动程序收到取消绑定通知、暂停指示、低能耗事件或 PD 配置更改事件（指示在绑定上禁用了 PD）时，它必须调用此 OID。

在调用此 OID 之前，NDIS 协议或筛选器驱动程序必须确保它已关闭并释放了通过 PD 提供程序实例创建的所有 PD 对象，例如队列、计数器和筛选器。 在发出此 OID 之前，NDIS 协议或筛选器驱动程序必须保证不存在对任何 PD 提供程序调度表函数的正在进行的调用。

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
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)

[**NDIS\_PD\_关闭\_提供程序\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_close_provider_parameters)

[NDIS\_状态\_PD\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pd-current-config)

[OID\_PD\_打开\_提供程序](oid-pd-open-provider.md)

 

 




