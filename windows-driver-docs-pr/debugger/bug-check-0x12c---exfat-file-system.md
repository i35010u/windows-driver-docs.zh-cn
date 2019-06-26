---
title: Bug 检查 0x12C EXFAT_FILE_SYSTEM
description: EXFAT_FILE_SYSTEM bug 检查具有 0x0000012C 值。 此 bug 检查指示扩展文件分配表 (exFAT) 文件系统中出现问题。
ms.assetid: f55bbe88-d96f-494f-b84b-eda7c4e6bdfc
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
ms.openlocfilehash: 9f13dce35d487c5aebf6ccdc7a6e041cbbda04e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362274"
---
# <a name="bug-check-0x12c-exfatfilesystem"></a>Bug 检查 0x12C：EXFAT\_FILE\_SYSTEM


EXFAT\_文件\_检查系统错误的值为 0x0000012C。 此 bug 检查指示扩展文件分配表 (exFAT) 文件系统中出现问题。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="exfatfilesystem-parameters"></a>EXFAT\_文件\_系统参数


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
<td align="left"><p>指定源代码文件和行号信息。 高 16 位 （"0x"后的前四个十六进制数） 确定按标识符号的源文件。 低 16 位确定发生错误检查的文件中的源行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>如果<strong>FppExceptionFilter</strong>是在堆栈上，此参数指定的地址的异常记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>如果<strong>FppExceptionFilter</strong>是在堆栈上，此参数指定的上下文记录的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此 bug 检查是由文件系统在最后迫不得已时引起其内部记帐处于不支持状态，若要继续会带来较大的数据丢失风险。 上的磁盘结构损坏、 磁盘扇区陷入困境，或内存分配失败时，文件系统永远不会导致此 bug 检查。 扇区损坏导致的 bug 检查，例如，内核代码中会发生页面故障或数据和内存管理器无法读取页时。 但是，对于此 bug 检查，文件系统不是原因。

<a name="resolution"></a>分辨率
----------

**若要调试此问题：** 使用[ **.cxr （显示上下文记录）** ](-cxr--display-context-record-.md)命令以及参数 3，并使用[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)。

 

 




