---
title: Bug 检查 0xF5 FLTMGR_FILE_SYSTEM
description: FLTMGR_FILE_SYSTEM bug 检查具有 0x000000F5 值。 这表明无法恢复的错误发生在筛选器管理器中。
ms.assetid: 9b008c76-65c8-4de4-b7a0-96d8732c7b7e
keywords:
- Bug 检查 0xF5 FLTMGR_FILE_SYSTEM
- FLTMGR_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- FLTMGR_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 81c2036fd621ffd6500429a7ce8bfb70ba4a0fa8
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239562"
---
# <a name="bug-check-0xf5-fltmgrfilesystem"></a>Bug 检查 0xF5：FLTMGR\_FILE\_SYSTEM


FLTMGR\_文件\_检查系统错误的值为 0x000000F5。 这表明无法恢复的错误发生在筛选器管理器中。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="fltmgrfilesystem-parameters"></a>FLTMGR\_文件\_系统参数


参数 1 指示冲突的类型。 其他参数的含义取决于参数 1 的值。

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
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x66</p></td>
<td align="left"><p>该操作的回调数据结构的指针。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>微筛选器返回 FLT_PREOP_SUCCESS_WITH_CALLBACK 或 FLT_PREOP_SYNCHRONIZE 从 preoperation 回调，但未注册相应的 postoperation 回调。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x67</p></td>
<td align="left"><p>该操作的回调数据结构的指针。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>操作错误 NTSTATUS 代码</p></td>
<td align="left"><p>内部对象用尽了空间，并且系统无法分配新空间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x68</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>FLT_FILE_NAME_INFORMATIONN 结构的地址</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>FLT_FILE_NAME_INFORMATION 结构已取消引用次数过多。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6A</p></td>
<td align="left"><p>对象文件的指针。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>文件打开或创建文件的请求无法取消，因为已为该文件创建了一个或多个句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6B</p></td>
<td align="left"><p>帧 ID</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>线程</p></td>
<td align="left"><p>BACKPOCKET IRPCTRL 状态无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6C</p></td>
<td align="left"><p>帧 ID</p></td>
<td align="left"><p>BackPocket 列表</p></td>
<td align="left"><p>线程</p></td>
<td align="left"><p>有关 BACKPOCKETED IRPCTR 太多嵌套的 PageFaults。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6D</p></td>
<td align="left"><p>微筛选器的上下文结构的地址</p></td>
<td align="left"><p>CONTEXT_NODE 结构的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>上下文结构已取消引用次数过多。 这意味着，它仍附加到与其关联的对象时，筛选器管理器的 CONTEXT_NODE 结构的引用计数出现了为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6E</p></td>
<td align="left"><p>微筛选器的上下文结构的地址</p></td>
<td align="left"><p>CONTEXT_NODE 结构的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>上下文结构被释放后引用。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

由参数 1 的值指示问题的原因。 请参阅参数部分中的表。

<a name="resolution"></a>分辨率
----------

如果参数 1 等于**0x66**，可以通过验证微筛选器驱动程序已注册此操作的操作后回调来调试此问题。 可以在回调数据结构中找到当前操作。 （请参阅参数 2。）使用 **！ fltkd.cbd**调试器扩展。

如果参数 1 等于**0x67**，应验证，您没有非分页缓冲的池泄漏某个位置在系统中。

如果参数 1 等于**0x6A**，请确保此文件不引用微筛选器驱动程序对象 （请参阅参数 2），以便你微筛选器处理此操作期间任何时候获取的句柄。

如果参数 1 等于**0x6B**或**0x6C**，则这将导致 bug 检查操作系统发生了不可恢复的内部状态错误。

如果参数 1 等于**0x6D**，请确保微筛选器驱动程序不会调用**FltReleaseContext**给定上下文的次数过多 （请参阅参数 2）。

如果参数 1 等于 0x6E，请确保微筛选器驱动程序不会调用**FltReferenceContext**删除给定的上下文之后 （请参阅参数 2）。

 

 




