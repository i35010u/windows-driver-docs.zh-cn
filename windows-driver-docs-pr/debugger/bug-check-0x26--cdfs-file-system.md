---
title: Bug 检查 0x26 CDFS_FILE_SYSTEM
description: CDFS_FILE_SYSTEM bug 检查具有 0x00000026 值。 这表示 CD 文件系统中出现问题。
ms.assetid: f427c262-f750-4719-a52b-2f00094d2a4e
keywords:
- Bug 检查 0x26 CDFS_FILE_SYSTEM
- CDFS_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CDFS_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8c9bacd493cab280338f56f458cf47b6adf76032
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367531"
---
# <a name="bug-check-0x26-cdfsfilesystem"></a>Bug 检查 0x26：CDFS\_FILE\_SYSTEM


CDFS\_文件\_检查系统错误的值为 0x00000026。 这表示 CD 文件系统中出现问题。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="cdfsfilesystem-parameters"></a>CDFS\_文件\_系统参数


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
<td align="left"><p>指定源代码文件和行号信息。 高 16 位 （"0x"后的前四个十六进制数字） 标识由其标识符编号的源代码文件。 低 16 位标识发生错误检查的文件中的源行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>如果<strong>CdExceptionFilter</strong>是在堆栈上，此参数指定的地址的异常记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>如果<strong>CdExceptionFilter</strong>是在堆栈上，此参数指定的上下文记录的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此 bug 检查的一个可能的原因是磁盘损坏。 文件系统或磁盘上的坏扇区 （扇区） 中的损坏可导致此错误。 损坏的 SCSI 和 IDE 驱动程序可能还会影响系统的能够读取和写入磁盘，从而导致错误。

另一个可能原因是非分页缓冲的池内存耗尽。 如果完全耗尽的非分页缓冲的池内存，则此错误可以停止系统。 但是，在索引过程中，如果可用的非分页缓冲的池内存量为非常低，需要非分页缓冲的池内存的另一个内核模式驱动程序还可以触发此错误。

<a name="resolution"></a>分辨率
----------

**若要调试此问题：** 使用[ **.cxr （显示上下文记录）** ](-cxr--display-context-record-.md)命令参数 3 中，并使用[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)。

**若要解决磁盘损坏问题：** 检查事件查看器从 SCSI 和 FASTFAT （系统日志） 或 Autochk （应用程序日志），可能会帮助找出设备或导致错误的驱动程序的错误消息。 请尝试禁用任何病毒扫描程序、 备份程序或持续监视系统的磁盘碎片整理程序工具。 您还应运行硬件诊断系统制造商提供。 有关这些过程的详细信息，请参阅您的计算机的所有者的手册。 运行**Chkdsk /f /r**检测和解决任何文件系统结构损坏。 系统分区上的磁盘扫描开始之前，必须重新启动系统。

**若要解决非分页缓冲的池内存耗尽问题：** 向计算机添加新的物理内存。 这会增加可用的内核的非分页缓冲的池内存的数量。

 

 




