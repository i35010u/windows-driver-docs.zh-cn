---
title: Bug 检查 0x108 THIRD_PARTY_FILE_SYSTEM_FAILURE
description: THIRD_PARTY_FILE_SYSTEM_FAILURE bug 检查的值为0x00000108。 这表示第三方文件系统或文件系统筛选器中发生了不可恢复的问题。
keywords:
- Bug 检查 0x108 THIRD_PARTY_FILE_SYSTEM_FAILURE
- THIRD_PARTY_FILE_SYSTEM_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- THIRD_PARTY_FILE_SYSTEM_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6dcb50fde359d9963c73b451dcf6a11689d39d89
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836897"
---
# <a name="bug-check-0x108-third_party_file_system_failure"></a>Bug 检查0x108：第三 \_ 方 \_ 文件 \_ 系统 \_ 失败


第三 \_ 方 \_ 文件 \_ 系统 \_ 失败 bug 检查的值为0x00000108。 这表示第三方文件系统或文件系统筛选器中发生了不可恢复的问题。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="third_party_file_system_failure-parameters"></a>第三 \_ 方 \_ 文件 \_ 系统 \_ 失败参数


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
<td align="left"><p>标识失败的文件系统。 可能的值包括：</p>
<p><strong>1：</strong> Polyserve ( # A0) </p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>异常记录的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>上下文记录的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此错误检查的一个可能原因是磁盘损坏。 第三方文件系统损坏或硬盘上的坏块 (扇) 区会导致此错误。 损坏的 SCSI 和 IDE 驱动程序也可能对 Windows 操作系统读写磁盘的能力产生负面影响，从而导致错误。

另一个可能的原因是消耗了未分页的池内存。 如果非分页池完全耗尽，此错误可能会停止系统。

<a name="resolution"></a>解决方法
----------

**若要调试此问题：** 使用参数 3 [**(显示上下文记录)**](-cxr--display-context-record-.md) 命令，然后使用 [**Kb (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)。

**解决磁盘损坏问题：** 检查来自系统中 SCSI、IDE 或其他磁盘控制器的错误消息事件查看器，这些错误消息可能有助于查明导致错误的设备或驱动程序。 尝试禁用持续监视系统的任何病毒扫描程序、备份程序或磁盘碎片整理程序工具。 还应运行文件系统或文件系统筛选器制造商提供的硬件诊断。

**解决非分页池内存消耗问题：** 向计算机添加新的物理内存。 这会增加可用于内核的非分页缓冲池内存量。

 

 




