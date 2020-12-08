---
title: Bug 检查 0xFA HTTP_DRIVER_CORRUPTED
description: 'HTTP_DRIVER_CORRUPTED bug 检查的值为0x000000FA。 这表示 HTTP 内核驱动程序 ( # A0) 已达到损坏状态，因此无法恢复。'
keywords:
- Bug 检查 0xFA HTTP_DRIVER_CORRUPTED
- HTTP_DRIVER_CORRUPTED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- HTTP_DRIVER_CORRUPTED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: de25578c0725250b6afdaf4420020a63229b1095
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805747"
---
# <a name="bug-check-0xfa-http_driver_corrupted"></a>Bug 检查0xFA： HTTP \_ 驱动程序 \_ 已损坏


HTTP \_ 驱动程序 \_ 损坏 bug 检查的值为0x000000FA。 这表示 HTTP 内核驱动程序 ( # A0) 已达到损坏状态，因此无法恢复。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="http_driver_corrupted-parameters"></a>HTTP \_ 驱动程序 \_ 损坏参数


参数1标识 HTTP 内核驱动程序的确切状态。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>工作项的地址</p></td>
<td align="left"><p>包含工作项检查的文件的名称</p></td>
<td align="left"><p>文件中工作项检查的行号</p></td>
<td align="left"><p>工作项无效。 这最终会导致线程池损坏和访问冲突。</p></td>
</tr>
</tbody>
</table>

 

 

 




