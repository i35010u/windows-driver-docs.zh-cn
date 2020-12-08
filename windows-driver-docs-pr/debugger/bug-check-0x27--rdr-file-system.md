---
title: Bug 检查 0x27 RDR_FILE_SYSTEM
description: RDR_FILE_SYSTEM bug 检查的值为0x00000027。 这表明 SMB 重定向程序文件系统中出现问题。
keywords:
- Bug 检查 0x27 RDR_FILE_SYSTEM
- RDR_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- RDR_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eee97e4680a5a82cf7758ff30649f2e771897ef8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824709"
---
# <a name="bug-check-0x27-rdr_file_system"></a>Bug 检查0x27： RDR \_ 文件 \_ 系统


RDR \_ 文件 \_ 系统 bug 检查的值为0x00000027。 这表明 SMB 重定向程序文件系统中出现问题。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="rdr_file_system-parameters"></a>RDR \_ 文件 \_ 系统参数


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
<td align="left"><p>高16位 ("0x" 后的前四个十六进制数字 ) 确定问题类型。 可能的值包括：</p>
<p>0xCA550000 RDBSS_BUG_CHECK_CACHESUP</p>
<p>0xC1EE0000 RDBSS_BUG_CHECK_CLEANUP</p>
<p>0xC10E0000 RDBSS_BUG_CHECK_CLOSE</p>
<p>0xBAAD0000 RDBSS_BUG_CHECK_NTEXCEPT</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>如果 <strong>RxExceptionFilter</strong> 位于堆栈上，则此参数指定异常记录的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>如果 <strong>RxExceptionFilter</strong> 位于堆栈上，则此参数指定上下文记录的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此错误检查的一个可能原因是消耗了未分页的池内存。 如果非分页池内存完全耗尽，此错误可能会停止系统。 但是，在索引过程中，如果可用的非分页池内存量非常低，则另一个需要非分页池内存的内核模式驱动程序也会触发此错误。

<a name="resolution"></a>解决方法
----------

**若要调试此问题：** 使用参数 3 [**(显示上下文记录)**](-cxr--display-context-record-.md) 命令，然后使用 [**Kb (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)。

**解决非分页池内存消耗问题：** 向计算机添加新的物理内存。 这会增加可用于内核的非分页缓冲池内存量。

 

 




