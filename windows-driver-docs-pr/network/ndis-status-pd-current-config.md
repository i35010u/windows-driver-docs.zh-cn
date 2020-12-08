---
title: NDIS_STATUS_PD_CURRENT_CONFIG
description: 此状态指示是 NDIS_PD_CONFIG 结构发生更改的通知。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PD_CURRENT_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a5b18d54c9dcb07d3eb2b3585003487d9339d617
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801501"
---
# <a name="ndis_status_pd_current_config"></a>NDIS \_ 状态 \_ PD \_ 当前 \_ 配置


此状态指示是 [**NDIS \_ PD \_ CONFIG**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pd_config) 结构已更改的通知。

支持 PacketDirect 的微型端口驱动程序必须 \_ \_ \_ \_ 在 [oid \_ pd \_ 关闭 \_ 提供程序](./oid-pd-close-provider.md) 或 [oid \_ pd \_ OPEN \_ provider](./oid-pd-open-provider.md) 请求后，使 NDIS 状态 PD 当前配置状态指示。

微型端口驱动程序调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)来进行状态指示，必须通过 *StatusIndication* 参数将指针传递到 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构。 做出此指示时，微型端口驱动程序必须设置以下 **NDIS \_ 状态 \_ 指示** 结构的成员：

-   必须将 **SourceHandle** 设置为 *MiniportAdapterHandle* 参数中 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数接收的句柄。

-   **StatusCode** 必须设置为 NDIS \_ 状态 \_ PD \_ 当前 \_ 配置。

-   **StatusBuffer** 必须设置为 ULONG 变量的地址，该变量为扫描操作的结果存储适当的 NDIS \_ 状态 \_ xxxx 代码。

-   必须将 **StatusBufferSize** 设置为 **sizeof** (ULONG) 。

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
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

[OID \_ PD \_ 关闭 \_ 提供程序](./oid-pd-close-provider.md)

[OID \_ PD \_ 打开 \_ 提供程序](./oid-pd-open-provider.md)

 

