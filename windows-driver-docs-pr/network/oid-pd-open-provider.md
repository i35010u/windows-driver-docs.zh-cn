---
title: OID_PD_OPEN_PROVIDER
description: NDIS 协议或筛选器驱动程序将对象标识符 (OID) 方法请求 OID_PD_OPEN_PROVIDER 发送到支持 PD 的微型端口驱动程序，以获取对微型端口驱动程序的 PDPI 提供程序对象中的 PD 功能的访问权限。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PD_OPEN_PROVIDER 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2c04a7b8fab78fe7da00ac3732cb11e5c2d9594c
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249045"
---
# <a name="oid_pd_open_provider"></a>OID \_ PD \_ 打开 \_ 提供程序


NDIS 协议或筛选器驱动程序将对象标识符 (OID 发送到支持 PD 的微型端口驱动程序的 OID) 方法请求发送到 \_ \_ 微型端口驱动程序 \_ 的 PDPI 提供程序对象。 所有支持 PD 的微型端口驱动程序都必须处理此 OID 请求。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向缓冲区的指针。 此缓冲区包含以下数据：

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)

[**NDIS \_ PD \_ 打开 \_ 提供程序 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_open_provider_parameters)

[NDIS \_ 状态 \_ PD \_ 当前 \_ 配置](./ndis-status-pd-current-config.md)

[OID \_ PD \_ 关闭 \_ 提供程序](oid-pd-close-provider.md)

 

