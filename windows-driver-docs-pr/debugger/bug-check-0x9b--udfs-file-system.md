---
title: Bug 检查 0x9B UDFS_FILE_SYSTEM
description: UDFS_FILE_SYSTEM bug 检查的值为0x0000009B。 此 bug 检查指示 UDF 文件系统中出现问题。
keywords:
- Bug 检查 0x9B UDFS_FILE_SYSTEM
- UDFS_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- UDFS_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fc50193fd5ff1fa944d8a2ea7ddbcd274d8f5b98
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839329"
---
# <a name="bug-check-0x9b-udfs_file_system"></a>Bug 检查0x9B： UDF \_ 文件 \_ 系统


UDF \_ 文件 \_ 系统 bug 检查的值为0x0000009B。 此 bug 检查指示 UDF 文件系统中出现问题。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="udfs_file_system-parameters"></a>UDF \_ 文件 \_ 系统参数


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
<td align="left"><p>源文件和行号信息。 高16位 ("0x" 后的前四个十六进制数字 ) 按其标识符号识别源文件。 低16位标识文件中发生错误检查的源行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>如果 <strong>UdfExceptionFilter</strong> 位于堆栈上，则此参数指定异常记录的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>如果 <strong>UdfExceptionFilter</strong> 位于堆栈上，则此参数指定上下文记录的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

UDF \_ 文件 \_ 系统 bug 检查可能会导致磁盘损坏。 文件系统损坏或坏块 (扇区) 会导致此错误。 损坏的 SCSI 和 IDE 驱动程序还可能会对系统读写磁盘和导致错误的能力产生负面影响。

如果非分页池内存已满，则也可能会发生此 bug 检查。 如果非分页池内存已满，此错误可能会停止系统。 但是，在索引过程中，如果可用的非分页池内存量非常低，则另一个需要非分页池内存的内核模式驱动程序也会触发此错误。

<a name="resolution"></a>解决方法
----------

**若要调试此问题：** 使用参数 3 [**(显示上下文记录)**](-cxr--display-context-record-.md) 命令，然后使用 [**Kb (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)。

**解决磁盘损坏问题：** 检查来自 SCSI 和 FASTFAT (系统日志) 或 Autochk (应用程序日志) 的错误消息事件查看器，这些错误消息可能有助于识别导致错误的设备或驱动程序。 禁用持续监视系统的任何病毒扫描程序、备份应用程序或磁盘碎片整理程序工具。 还应运行系统制造商提供的硬件诊断。 有关这些过程的详细信息，请参阅您的计算机的所有者手册。 运行 **Chkdsk/f/r** 来检测和解决任何文件系统结构损坏。 在系统分区上开始磁盘扫描之前，必须重启系统。

**解决非分页池内存消耗问题：** 向计算机添加新的物理内存。 此内存增加了可用于内核的非分页缓冲池的内存量。

 

 




