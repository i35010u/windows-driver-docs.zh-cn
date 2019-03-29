---
title: MB 微型端口驱动程序错误日志记录
description: MB 微型端口驱动程序错误日志记录
ms.assetid: 57f83d03-29e5-4a20-8c0c-2d00954e7ccb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 015bf2fe6831729d7a624c2bc938751cb89f48f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566027"
---
# <a name="mb-miniport-driver-error-logging"></a>MB 微型端口驱动程序错误日志记录


MB 微型端口驱动程序应执行以下检查中的其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数，例如：

-   存在支持 MB 驱动程序模型所需的正确的设备固件版本。

-   可用来与设备通信的 COM 端口。

-   没有资源冲突。

如果微型端口驱动程序无法获取它需要的资源，则应返回 NDIS\_状态\_其 MiniportInitializeEx 函数中的资源。 微型端口驱动程序应调用[ **NdisWriteErrorLogEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff564663)记录到 Windows 事件日志中的失败的详细信息。

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

 

 





