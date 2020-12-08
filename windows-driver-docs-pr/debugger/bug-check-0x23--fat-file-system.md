---
title: Bug 检查 0x23 FAT_FILE_SYSTEM
description: FAT_FILE_SYSTEM bug 检查的值为0x00000023。 这表明 FAT 文件系统中出现问题。
keywords:
- Bug 检查 0x23 FAT_FILE_SYSTEM
- FAT_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- FAT_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cf6a979b4022c7f384a1e9c575e62f18f2896373
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839807"
---
# <a name="bug-check-0x23-fat_file_system"></a>Bug 检查0x23： FAT \_ 文件 \_ 系统


FAT \_ 文件 \_ 系统 bug 检查的值为0x00000023。 这表明 FAT 文件系统中出现问题。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="fat_file_system-parameters"></a>FAT \_ 文件 \_ 系统参数


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
<td align="left"><p>指定源文件和行号信息。 高16位 ("0x" 后的前四个十六进制数字 ) 按其标识符号识别源文件。 低16位标识文件中发生错误检查的源行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>如果 <strong>FatExceptionFilter</strong> 位于堆栈上，则此参数指定异常记录的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>如果 <strong>FatExceptionFilter</strong> 位于堆栈上，则此参数指定上下文记录的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此错误检查的一个可能原因是磁盘损坏。 文件系统损坏或坏块 (扇区) 会导致此错误。 损坏的 SCSI 和 IDE 驱动程序也可能对系统读写磁盘的能力产生负面影响，从而导致错误。

另一个可能的原因是消耗了未分页的池内存。 如果非分页池内存完全耗尽，此错误可能会停止系统。 但是，在索引过程中，如果可用的非分页池内存量非常低，则另一个需要非分页池内存的内核模式驱动程序也会触发此错误。

<a name="resolution"></a>解决方法
----------

**若要调试此问题：** 使用参数 3 [**(显示上下文记录)**](-cxr--display-context-record-.md) 命令，然后使用 [**Kb (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)。

**解决磁盘损坏问题：** 检查来自 SCSI 和 FASTFAT (系统日志) 或 Autochk (应用程序日志) 的错误消息事件查看器，这些错误消息可能有助于找出导致错误的设备或驱动程序。 尝试禁用持续监视系统的任何病毒扫描程序、备份程序或磁盘碎片整理程序工具。 还应运行系统制造商提供的硬件诊断。 有关这些过程的详细信息，请参阅计算机的用户手册。 运行 **Chkdsk/f/r** 来检测和解决任何文件系统结构损坏。 在系统分区上开始磁盘扫描之前，必须重启系统。

**解决非分页池内存消耗问题：** 向计算机添加新的物理内存。 这会增加可用于内核的非分页缓冲池内存量。

 

 




