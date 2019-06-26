---
title: NDIS_STATUS_PD_CURRENT_CONFIG
description: 此状态指示是 NDIS_PD_CONFIG 结构已更改的通知。
ms.assetid: 0B63E85E-36A8-4DC4-A060-C40DCB6BE454
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PD_CURRENT_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1267564707c0a8dfee868eadbd3e064ea9ae8f15
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368539"
---
# <a name="ndisstatuspdcurrentconfig"></a>NDIS\_状态\_PD\_当前\_配置


此状态指示是一个通知， [ **NDIS\_PD\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pd_config)结构已更改。

支持 PacketDirect 的微型端口驱动程序必须进行 NDIS\_状态\_PD\_当前\_后的配置状态指示[OID\_PD\_关闭\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pd-close-provider)或[OID\_PD\_打开\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pd-open-provider)请求。

微型端口驱动程序调用[ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)以使状态指示，并且必须通过一个指向[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构，通过*StatusIndication*参数。 微型端口驱动程序时进行这种指示，必须设置的以下成员**NDIS\_状态\_指示**结构：

-   **SourceHandle**必须设置为微型端口接收中的句柄*MiniportAdapterHandle*参数[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。

-   **StatusCode**必须设置为 NDIS\_状态\_PD\_当前\_配置。

-   **StatusBuffer**必须设置为将存储相应 NDIS ULONG 变量的地址\_状态\_xxxx 扫描操作的结果代码。

-   **StatusBufferSize**必须设置为**sizeof**(ULONG)。

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
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)

[OID\_PD\_关闭\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pd-close-provider)

[OID\_PD\_打开\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pd-open-provider)

 

 




