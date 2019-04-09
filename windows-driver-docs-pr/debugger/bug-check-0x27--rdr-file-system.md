---
title: Bug 检查 0x27 RDR_FILE_SYSTEM
description: RDR_FILE_SYSTEM bug 检查具有 0x00000027 值。 这表示 SMB 重定向程序文件系统中出现问题。
ms.assetid: 1294022d-7281-45d2-89c8-40d11ce202f0
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
ms.openlocfilehash: faed326e57c284b4c1bad5dc070386bb4510465a
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238980"
---
# <a name="bug-check-0x27-rdrfilesystem"></a>Bug 检查 0x27：RDR\_FILE\_SYSTEM


RDR\_文件\_检查系统错误的值为 0x00000027。 这表示 SMB 重定向程序文件系统中出现问题。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="rdrfilesystem-parameters"></a>RDR\_文件\_系统参数


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
<td align="left"><p>高 16 位 （"0x"后的前四个十六进制数） 确定的问题的类型。 可能值的包括：</p>
<p>0xCA550000 RDBSS_BUG_CHECK_CACHESUP</p>
<p>0xC1EE0000 RDBSS_BUG_CHECK_CLEANUP</p>
<p>0xC10E0000 RDBSS_BUG_CHECK_CLOSE</p>
<p>0xBAAD0000 RDBSS_BUG_CHECK_NTEXCEPT</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>如果<strong>RxExceptionFilter</strong>是在堆栈上，此参数指定的地址的异常记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>如果<strong>RxExceptionFilter</strong>是在堆栈上，此参数指定的上下文记录的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此 bug 检查的一个可能的原因是非分页缓冲的池内存耗尽。 如果完全耗尽的非分页缓冲的池内存，则此错误可以停止系统。 但是，在索引过程中，如果可用的非分页缓冲的池内存量为非常低，需要非分页缓冲的池内存的另一个内核模式驱动程序还可以触发此错误。

<a name="resolution"></a>分辨率
----------

**若要调试此问题：** 使用[ **.cxr （显示上下文记录）** ](-cxr--display-context-record-.md)命令参数 3 中，并使用[ **kb （显示堆栈回溯）**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)。

**若要解决非分页缓冲的池内存耗尽问题：** 向计算机添加新的物理内存。 这会增加可用的内核的非分页缓冲的池内存的数量。

 

 




