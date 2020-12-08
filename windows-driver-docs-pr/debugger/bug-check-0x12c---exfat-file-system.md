---
title: Bug 检查 0x12C EXFAT_FILE_SYSTEM
description: EXFAT_FILE_SYSTEM bug 检查的值为0x0000012C。 此 bug 检查指示扩展文件分配表中出现问题 (exFAT) 文件系统。
keywords:
- Bug 检查 0x12C EXFAT_FILE_SYSTEM
- EXFAT_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- EXFAT_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 01e755e6386a3ca3214f86c13b836e47b05a84e5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839961"
---
# <a name="bug-check-0x12c-exfat_file_system"></a>Bug 检查0x12C： EXFAT \_ 文件 \_ 系统


EXFAT \_ 文件 \_ 系统 bug 检查的值为0x0000012C。 此 bug 检查指示扩展文件分配表中出现问题 (exFAT) 文件系统。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="exfat_file_system-parameters"></a>EXFAT \_ 文件 \_ 系统参数


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
<td align="left"><p>指定源文件和行号信息。 高16位 ("0x" 后的前四个十六进制数字 ) 按其标识符号确定源文件。 低16位确定文件中发生错误检查的源行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>如果 <strong>FppExceptionFilter</strong> 位于堆栈上，则此参数指定异常记录的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>如果 <strong>FppExceptionFilter</strong> 位于堆栈上，则此参数指定上下文记录的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此 bug 检查是由文件系统在其内部记帐处于似乎状态时作为最后一种手段引起的，并且继续会导致数据丢失的风险大。 当磁盘结构损坏、磁盘扇区损坏或内存分配失败时，文件系统永远不会导致此错误检查。 坏扇区可能导致错误检查，例如，当内核代码或数据中出现页面错误时，内存管理器无法读取页面。 但对于此错误检查，文件系统不是原因。

<a name="resolution"></a>解决方法
----------

**若要调试此问题：** 使用 [**.cxr (显示上下文记录)**](-cxr--display-context-record-.md) 命令以及参数3，然后使用 [**Kb (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)。

 

 




