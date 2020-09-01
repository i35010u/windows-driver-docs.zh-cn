---
title: OID_PD_OPEN_PROVIDER
description: NDIS 协议或筛选器驱动程序将对象标识符 (OID) 方法请求 OID_PD_OPEN_PROVIDER 发送到支持 PD 的微型端口驱动程序，以获取对微型端口驱动程序的 PDPI 提供程序对象中的 PD 功能的访问权限。
ms.assetid: B13E0FAC-A179-4785-9B39-CB498064947B
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PD_OPEN_PROVIDER 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3145adb3f7d49d3353b32a0542a5dcafac2d214f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210619"
---
# <a name="oid_pd_open_provider"></a>OID \_ PD \_ 打开 \_ 提供程序


NDIS 协议或筛选器驱动程序将对象标识符 (OID 发送到支持 PD 的微型端口驱动程序的 OID) 方法请求发送到 \_ \_ 微型端口驱动程序 \_ 的 PDPI 提供程序对象。 所有支持 PD 的微型端口驱动程序都必须处理此 OID 请求。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [**NDIS \_ PD \_ 打开 \_ 提供程序 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_open_provider_parameters)结构

<a name="remarks"></a>备注
-------

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
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)

[**NDIS \_ PD \_ 打开 \_ 提供程序 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_open_provider_parameters)

[NDIS \_ 状态 \_ PD \_ 当前 \_ 配置](./ndis-status-pd-current-config.md)

[OID \_ PD \_ 关闭 \_ 提供程序](oid-pd-close-provider.md)

 

