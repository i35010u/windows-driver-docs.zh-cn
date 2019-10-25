---
title: NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG 状态指示通知 NDIS 和过量驱动程序已更改了 NIC 的任务卸载配置。
ms.assetid: 8a098dff-409e-4168-a3aa-372851aa999d
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e4dfff15f00209884b882ab74ce996dd2815b273
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843510"
---
# <a name="ndis_status_task_offload_current_config"></a>\_任务\_卸载\_当前\_配置的 NDIS\_状态


小型端口驱动程序使用**NDIS\_状态\_任务\_卸载\_当前\_配置**状态指示，以通知 NDIS 和过量驱动程序已更改 NIC 的任务卸载配置。

<a name="remarks"></a>备注
-------

小型端口驱动程序必须在当前功能发生更改时，用**NDIS\_状态报告当前功能\_任务\_卸载\_当前\_配置**状态指示。 此状态指示可确保所有的过量协议驱动程序都用新功能信息进行更新。 在以下情况下，需要微型端口驱动程序来发出此状态指示：

1.  当微型端口驱动程序接收[OID\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)设置请求时，它必须使用[**NDIS\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)结构的内容来更新当前启用的任务卸载功能.
2.  当微型端口驱动程序收到[OID\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)集请求时，它必须使用[**NDIS\_卸载\_封装**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation)结构的内容来更新当前启用的任务卸载功能.

[**Ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含[**ndis\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构。 发出**NDIS\_状态时\_任务\_卸载\_当前\_配置**状态指示，微型端口驱动程序必须使用**NDIS\_卸载**结构来报告当前的任务卸载配置的。

**请注意**  [**NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构的内容仅反映 NIC 的当前任务卸载配置，而不是其实际硬件功能。

 

有关当前任务卸载配置的详细信息，请参阅[OID\_TCP\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 NDIS 6.0 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)

[ **\_封装的 NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation)

[**NDIS\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[ **\_任务\_卸载\_硬件\_功能的 NDIS\_状态**](ndis-status-task-offload-hardware-capabilities.md)

[OID\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)

[OID\_TCP\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)

[OID\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)

 

 




