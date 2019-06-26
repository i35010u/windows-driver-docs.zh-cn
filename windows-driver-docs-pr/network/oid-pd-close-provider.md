---
title: OID_PD_CLOSE_PROVIDER
description: NDIS 协议或筛选器驱动程序将 OID_PD_CLOSE_PROVIDER 的对象标识符 (OID) 方法请求发送到 PDPI 提供商提供对 PDPI 提供程序对象中的 PD 功能的访问。
ms.assetid: 8A504A81-6DC8-415C-9FDC-F03657A0EB87
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PD_CLOSE_PROVIDER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7f321b3903fe5b21e8ba453db847c6d18f6c3e32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383244"
---
# <a name="oidpdcloseprovider"></a>OID\_PD\_关闭\_提供程序


NDIS 协议或筛选器驱动程序将发送对象标识符 (OID) 方法请求的 OID\_PD\_关闭\_到 PDPI 提供程序，以便对 PDPI 提供程序对象中的 PD 功能的访问提供程序。

NDIS 协议或筛选器驱动程序必须调用此 OID，当它收到取消绑定通知、 暂停指示、 低电源事件或指示 PD 禁用在绑定上的 PD 配置更改事件。

在调用之前此 OID，NDIS 协议或筛选器驱动程序必须确保它已关闭并释放所有 PD 对象，例如队列、 计数器和它对 PD 提供程序实例创建的筛选器。 NDIS 协议或筛选器驱动程序必须保证有任何正在进行中调用任何 PD 提供程序调度表函数之前发出此 OID。

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
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)

[**NDIS\_PD\_关闭\_提供程序\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_close_provider_parameters)

[NDIS\_状态\_PD\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pd-current-config)

[OID\_PD\_打开\_提供程序](oid-pd-open-provider.md)

 

 




