---
title: MB 微型端口驱动程序错误日志记录
description: MB 微型端口驱动程序错误日志记录
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 185ec42452d2e9d1168bcf7de11cb924146e03aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791417"
---
# <a name="mb-miniport-driver-error-logging"></a>MB 微型端口驱动程序错误日志记录


MB 微型端口驱动程序应在其 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数中执行以下检查，例如：

-   是否存在支持 MB 驱动程序模型所需的正确设备固件版本。

-   用于与设备进行通信的可用 COM 端口。

-   无资源冲突。

如果微型端口驱动程序未能获得它所需的资源，它应该 \_ \_ 从其 MiniportInitializeEx 函数返回 NDIS 状态资源。 微型端口驱动程序应调用 [**NdisWriteErrorLogEntry**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswriteerrorlogentry) ，将失败的详细信息记录到 Windows 事件日志中。

小型端口驱动程序应在对 NdisWriteErrorLogEntry 的调用中的第一个元素中指定错误代码，并根据下表中的信息 (ULONGs) 可变大小的数组。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">错误代码</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WWAN_ERROR_UNSUPPORTED_FIRMWARE</p></td>
<td align="left"><p>设备正在运行不受支持的固件版本。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_ERROR_COM_PORT_CONFLICT</p></td>
<td align="left"><p>无法打开 COM 端口用于与设备进行通信。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_ERROR_RESOURCE_CONFLICT_OTHER</p></td>
<td align="left"><p>任何其他资源冲突。</p></td>
</tr>
</tbody>
</table>

 

微型端口驱动程序可以在可变大小的数组的其余元素中放置其他值。

 

