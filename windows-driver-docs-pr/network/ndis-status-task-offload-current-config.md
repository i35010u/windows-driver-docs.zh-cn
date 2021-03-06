---
title: NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG 状态指示通知 NDIS 和过量驱动程序已更改了 NIC 的任务卸载配置。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 27ef0930b95655eab0017837d65eb7fe237e2cd2
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247749"
---
# <a name="ndis_status_task_offload_current_config"></a>NDIS \_ 状态 \_ 任务 \_ 卸载 \_ 当前 \_ 配置


微型端口驱动程序使用 **NDIS \_ 状态任务 " \_ \_ 卸载 \_ 当前 \_ 配置** 状态指示" 通知 NDIS 和过量驱动程序已更改 NIC 的任务卸载配置。

<a name="remarks"></a>备注
-------

小型端口驱动程序必须在当前功能发生更改时，用 **NDIS \_ 状态 \_ 任务 " \_ 卸载 \_ 当前 \_ 配置** 状态指示" 报告当前功能。 此状态指示可确保所有的过量协议驱动程序都用新功能信息进行更新。 在以下情况下，需要微型端口驱动程序来发出此状态指示：

1.  当微型端口驱动程序收到 [OID \_ TCP \_ 卸载 \_ 参数](./oid-tcp-offload-parameters.md) set 请求时，它必须使用 [**NDIS \_ 卸载 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters) 结构的内容来更新当前启用的任务卸载功能。
2.  当微型端口驱动程序收到 [OID \_ 卸载 \_ 封装](./oid-offload-encapsulation.md) 集请求时，它必须使用 [**NDIS \_ 卸载 \_ 封装**](/windows-hardware/drivers/ddi/encapsulationconfig/ns-encapsulationconfig-ndis_offload_encapsulation) 结构的内容来更新当前启用的任务卸载功能。

[**Ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的 **StatusBuffer** 成员包含 [**ndis \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构。 发出 **NDIS \_ 状态任务 " \_ \_ 卸载 \_ 当前 \_ 配置** 状态指示" 时，微型端口驱动程序必须使用 **NDIS \_ 卸载** 结构来报告 NIC 的当前任务卸载配置。

**注意** [**NDIS \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload) 结构的内容仅反映 NIC 的当前任务卸载配置，而不是其实际硬件功能。

 

有关当前任务卸载配置的详细信息，请参阅 [OID \_ TCP \_ 卸载 \_ 当前 \_ 配置](./oid-tcp-offload-current-config.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 NDIS 6.0 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)

[**NDIS \_ 卸载 \_ 封装**](/windows-hardware/drivers/ddi/encapsulationconfig/ns-encapsulationconfig-ndis_offload_encapsulation)

[**NDIS \_ 卸载 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS \_ 状态 \_ 任务 \_ 卸载 \_ 硬件 \_ 功能**](ndis-status-task-offload-hardware-capabilities.md)

[OID \_ 卸载 \_ 封装](./oid-offload-encapsulation.md)

[OID \_ TCP \_ 卸载 \_ 当前 \_ 配置](./oid-tcp-offload-current-config.md)

[OID \_ TCP \_ 卸载 \_ 参数](./oid-tcp-offload-parameters.md)

 

