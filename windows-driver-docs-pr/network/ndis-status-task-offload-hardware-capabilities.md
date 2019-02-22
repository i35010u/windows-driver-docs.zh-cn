---
title: NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES
description: NDIS 微型端口驱动程序和 MUX 中间驱动程序使用 NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES 状态指示通知 NDIS 和基础驱动程序已在任务中的更改卸载硬件功能的基础的 nic。
ms.assetid: 9ac8f4c9-66f4-4889-932b-a51381c54734
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4f77ee6c3844009a7f23c31dc1bbd97946a17a07
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523957"
---
# <a name="ndisstatustaskoffloadhardwarecapabilities"></a>NDIS\_状态\_任务\_卸载\_硬件\_功能


NDIS 微型端口驱动程序和 MUX 驱动程序使用的中间**NDIS\_状态\_任务\_卸载\_硬件\_功能**状态指示通知 NDIS和基础驱动程序已在任务中的更改卸载硬件功能的基础的 nic。

<a name="remarks"></a>备注
-------

如果在添加或删除基础 NIC，可以更改与微型端口驱动程序或 MUX 中间驱动程序相关联的总体硬件功能集。 例如，如果微型端口驱动程序将发出**NDIS\_状态\_任务\_卸载\_硬件\_功能**状态指示，它不能指定支持大量发送卸载 (LSO)，NIC 不再可配置为支持 LSO。

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构包含[ **NDIS\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566599)结构。 此结构指定任务卸载的硬件功能。

有关任务卸载硬件功能的详细信息，请参阅[OID\_TCP\_卸载\_硬件\_功能](https://msdn.microsoft.com/library/windows/hardware/ff569806)。

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
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_OFFLOAD**](https://msdn.microsoft.com/library/windows/hardware/ff566599)

[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_状态\_任务\_卸载\_当前\_配置**](ndis-status-task-offload-current-config.md)

[OID\_TCP\_卸载\_硬件\_功能](https://msdn.microsoft.com/library/windows/hardware/ff569806)

 

 




