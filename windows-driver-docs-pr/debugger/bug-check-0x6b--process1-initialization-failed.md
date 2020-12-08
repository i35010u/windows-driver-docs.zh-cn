---
title: Bug 检查 0x6B PROCESS1_INITIALIZATION_FAILED
description: PROCESS1_INITIALIZATION_FAILED bug 检查的值为0x0000006B。 此 bug 检查表明 Microsoft Windows 操作系统的初始化失败。
keywords:
- Bug 检查 0x6B PROCESS1_INITIALIZATION_FAILED
- PROCESS1_INITIALIZATION_FAILED
ms.date: 06/27/2018
topic_type:
- apiref
api_name:
- PROCESS1_INITIALIZATION_FAILED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 27fa36dec51b839b331b14ffa532dce7e844cef5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840849"
---
# <a name="bug-check-0x6b-process1_initialization_failed"></a>Bug 检查0x6B： PROCESS1 \_ 初始化 \_ 失败


PROCESS1 \_ 初始化 \_ 失败 bug 检查的值为0x0000006B。 此 bug 检查表明 Microsoft Windows 操作系统的初始化失败。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="process1_initialization_failed-parameters"></a>PROCESS1 \_ 初始化 \_ 失败参数


以下参数将出现在蓝色屏幕上。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>导致故障的 NT 状态代码</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

磁盘子系统的任何部分都可能会导致 PROCESS1 \_ 初始化 \_ 失败的错误检查，其中包括错误磁盘、错误或不正确的电缆、将不同 ATA 类型设备混合到相同链上，或在硬件重新生成时不可用的驱动器上。

此 bug 检查还可能是由于启动分区缺少文件，或是由某个用户在 " **驱动程序** " 选项卡中意外禁用的驱动程序引起的。

 
## <a name="resolution"></a>解决方法
[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。 




