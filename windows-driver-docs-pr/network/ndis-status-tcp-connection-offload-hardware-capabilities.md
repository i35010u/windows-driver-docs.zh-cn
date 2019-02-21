---
title: NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES
description: MUX 中间驱动程序使用 NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES 功能状态指示通知 NDIS 和基础驱动程序已在连接中的更改将卸载的基础硬件特征.
ms.assetid: 694cc0c4-0987-4095-8490-14ddfc9eaedb
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4a97a33ab6ca824dcf7045bc36b9edc902feb34d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524785"
---
# <a name="ndisstatustcpconnectionoffloadhardwarecapabilities"></a>NDIS\_状态\_TCP\_连接\_卸载\_硬件\_功能


MUX 中间驱动程序使用 NDIS\_状态\_TCP\_连接\_卸载\_硬件\_功能功能状态指示通知 NDIS 和基础驱动程序已在基础硬件连接卸载特征中的更改。

<a name="remarks"></a>备注
-------

如果在添加或删除基础 NIC，可以更改与 MUX 中间驱动程序相关联的总体硬件功能集。

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构包含[ **NDIS\_TCP\_连接\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff567875)结构。 NDIS\_TCP\_连接\_卸载指定任务卸载的硬件功能。

有关任务卸载硬件功能的详细信息，请参阅[OID\_TCP\_连接\_卸载\_硬件\_功能](https://msdn.microsoft.com/library/windows/hardware/ff569803)。

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


[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_TCP\_连接\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff567875)

[OID\_TCP\_连接\_卸载\_硬件\_功能](https://msdn.microsoft.com/library/windows/hardware/ff569803)

 

 




