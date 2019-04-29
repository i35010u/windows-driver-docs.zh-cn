---
title: NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG 状态指示通知发生了更改任务卸载的 NIC 配置 NDIS 和基础驱动程序
ms.assetid: 8a098dff-409e-4168-a3aa-372851aa999d
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 26a5655a658ab48030c2bb41e0903e25a7dce706
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361061"
---
# <a name="ndisstatustaskoffloadcurrentconfig"></a>NDIS\_状态\_任务\_卸载\_当前\_配置


微型端口驱动程序使用**NDIS\_状态\_任务\_卸载\_当前\_配置**状态指示通知 NDIS 和已有的基础驱动程序更改任务卸载配置中的 nic。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须报告与当前 capabilities **NDIS\_状态\_任务\_卸载\_当前\_配置**状态指示当前记录功能更改。 此状态指示可确保所有基础协议驱动程序使用新的功能信息更新。 微型端口驱动程序需要发出此状态指示在以下情况下：

1.  当微型端口驱动程序收到[OID\_TCP\_卸载\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569807)集请求，它必须使用的内容[ **NDIS\_卸载\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566706)结构，以更新当前已启用任务卸载功能。
2.  当微型端口驱动程序收到[OID\_卸载\_封装](https://msdn.microsoft.com/library/windows/hardware/ff569762)集请求，它必须使用的内容[ **NDIS\_卸载\_封装**](https://msdn.microsoft.com/library/windows/hardware/ff566702)结构，以更新当前已启用任务卸载功能。

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构包含[ **NDIS\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566599)结构。 在发出**NDIS\_状态\_任务\_卸载\_当前\_配置**微型端口驱动程序必须使用状态指示**NDIS\_卸载**到当前任务卸载的 NIC 配置的报表的结构

**请注意**  的内容[ **NDIS\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566599)结构反映仅 NIC 的当前任务卸载配置中，不是其实际硬件功能。

 

有关当前任务卸载配置的详细信息，请参阅[OID\_TCP\_卸载\_当前\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805)。

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
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_OFFLOAD**](https://msdn.microsoft.com/library/windows/hardware/ff566599)

[**NDIS\_卸载\_封装**](https://msdn.microsoft.com/library/windows/hardware/ff566702)

[**NDIS\_卸载\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566706)

[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_状态\_任务\_卸载\_硬件\_功能**](ndis-status-task-offload-hardware-capabilities.md)

[OID\_卸载\_封装](https://msdn.microsoft.com/library/windows/hardware/ff569762)

[OID\_TCP\_卸载\_当前\_配置](https://msdn.microsoft.com/library/windows/hardware/ff569805)

[OID\_TCP\_OFFLOAD\_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff569807)

 

 




