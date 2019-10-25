---
title: NDIS_STATUS_PD_CURRENT_CONFIG
description: 此状态指示是 NDIS_PD_CONFIG 结构已更改的通知。
ms.assetid: 0B63E85E-36A8-4DC4-A060-C40DCB6BE454
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PD_CURRENT_CONFIG 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6804254fae8e70074525778117d7226649e23ece
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842775"
---
# <a name="ndis_status_pd_current_config"></a>NDIS\_状态\_PD\_当前\_配置


此状态指示是指[**NDIS\_PD\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pd_config)结构已更改的通知。

支持 PacketDirect 的微型端口驱动程序必须将 NDIS\_状态\_PD\_当前\_CONFIG 状态指示之后， [oid\_pd\_关闭\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pd-close-provider)或[oid\_11_ 提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pd-open-provider)请求。

微型端口驱动程序调用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)来进行状态指示，必须通过*StatusIndication*参数将指向[**NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)的指针传递\_指示结构。 做出此指示时，微型端口驱动程序必须将**NDIS\_状态**的以下成员设置\_指示结构：

-   必须将**SourceHandle**设置为*MiniportAdapterHandle*参数中[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数接收的句柄。

-   必须将**StatusCode**设置为 NDIS\_状态\_PD\_当前\_配置。

-   必须将**StatusBuffer**设置为 ULONG 变量的地址，该变量为扫描操作的结果存储适当的 NDIS\_状态\_xxxx 代码。

-   **StatusBufferSize**必须设置为**sizeof**（ULONG）。

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
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

[OID\_PD\_关闭\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pd-close-provider)

[OID\_PD\_打开\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pd-open-provider)

 

 




