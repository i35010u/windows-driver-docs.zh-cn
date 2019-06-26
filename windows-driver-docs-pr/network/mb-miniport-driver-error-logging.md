---
title: MB 微型端口驱动程序错误日志记录
description: MB 微型端口驱动程序错误日志记录
ms.assetid: 57f83d03-29e5-4a20-8c0c-2d00954e7ccb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 318916f6d7cb1acd42bea89b5e43830823e495cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357793"
---
# <a name="mb-miniport-driver-error-logging"></a>MB 微型端口驱动程序错误日志记录


MB 微型端口驱动程序应执行以下检查中的其[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数，例如：

-   存在支持 MB 驱动程序模型所需的正确的设备固件版本。

-   可用来与设备通信的 COM 端口。

-   没有资源冲突。

如果微型端口驱动程序无法获取它需要的资源，则应返回 NDIS\_状态\_其 MiniportInitializeEx 函数中的资源。 微型端口驱动程序应调用[ **NdisWriteErrorLogEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiswriteerrorlogentry)记录到 Windows 事件日志中的失败的详细信息。

微型端口驱动程序应根据下表中的信息对 NdisWriteErrorLogEntry （可变大小的数组 ULONGs） 的调用中的最后一个参数的第一个元素中指定的错误代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">错误代码</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WWAN_ERROR_UNSUPPORTED_FIRMWARE</p></td>
<td align="left"><p>设备运行的是不受支持的固件版本。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_ERROR_COM_PORT_CONFLICT</p></td>
<td align="left"><p>无法打开与设备进行通信的 COM 端口。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_ERROR_RESOURCE_CONFLICT_OTHER</p></td>
<td align="left"><p>任何其他资源冲突。</p></td>
</tr>
</tbody>
</table>

 

微型端口驱动程序可以将其他值放在大小可变的数组的元素的其余部分。

 

 





