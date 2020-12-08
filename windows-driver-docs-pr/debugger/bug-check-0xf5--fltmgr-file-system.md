---
title: Bug 检查 0xF5 FLTMGR_FILE_SYSTEM
description: FLTMGR_FILE_SYSTEM bug 检查的值为0x000000F5。 这表明筛选器管理器中发生了不可恢复的错误。
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
ms.openlocfilehash: 5458177c7adb0d9ba3e612f771aa80e11cccc7ca
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824667"
---
# <a name="bug-check-0xf5-fltmgr_file_system"></a>Bug 检查0xF5： FLTMGR \_ 文件 \_ 系统


FLTMGR \_ 文件 \_ 系统 bug 检查的值为0x000000F5。 这表明筛选器管理器中发生了不可恢复的错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="fltmgr_file_system-parameters"></a>FLTMGR \_ 文件 \_ 系统参数


参数1指示违规类型。 其他参数的意义取决于参数1的值。

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
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x66</p></td>
<td align="left"><p>指向操作的回调数据结构的指针。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>微筛选器从 preoperation 回调返回 FLT_PREOP_SUCCESS_WITH_CALLBACK 或 FLT_PREOP_SYNCHRONIZE，但未注册相应的 postoperation 回调。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x67</p></td>
<td align="left"><p>指向操作的回调数据结构的指针。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>操作的错误 NTSTATUS 代码</p></td>
<td align="left"><p>内部对象用尽了空间，系统无法分配新的空间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x68</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>FLT_FILE_NAME_INFORMATIONN 结构的地址</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>取消引用 FLT_FILE_NAME_INFORMATION 结构的次数太多。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6A</p></td>
<td align="left"><p>文件的文件对象指针。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>由于已为文件创建一个或多个句柄，无法取消文件打开或文件创建请求。</p></td>
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
<td align="left"><p>嵌套的 PageFaults 对于 BACKPOCKETED IRPCTR 太多。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6D</p></td>
<td align="left"><p>微筛选器的上下文结构地址</p></td>
<td align="left"><p>CONTEXT_NODE 结构的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>上下文结构被取消引用的次数太多。 这意味着筛选器管理器的 CONTEXT_NODE 结构的引用计数在仍附加到其关联对象时将变为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6E</p></td>
<td align="left"><p>微筛选器的上下文结构地址</p></td>
<td align="left"><p>CONTEXT_NODE 结构的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>上下文结构在释放后被引用。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此问题的原因由参数1的值指示。 请参阅参数部分中的表。

<a name="resolution"></a>解决方法
----------

如果参数1等于 **0x66**，则可以通过验证微筛选器驱动程序是否已为此操作注册了操作后回调来调试此问题。 当前操作可在回调数据结构中找到。  (参见参数 2. ) 使用 **！ cbd** 调试器扩展。

如果参数1等于 **0x67**，则应验证是否在系统中的某个位置没有非分页池泄露。

如果参数1等于 **0x6A**，请确保你的微筛选器驱动程序不引用此文件对象 (请参阅参数 2) 在你的微筛选器处理此操作过程中的任何时间点获取句柄。

如果参数1等于 **0x6B** 或 **0x6C**，则发生了将导致操作系统 bug 检查的不可恢复的内部状态错误。

如果参数1等于 **0x6D**，请确保微筛选器驱动程序不会针对给定的上下文调用 **FltReleaseContext** 太多次 (参阅参数 2) 。

如果参数1等于0x6E，请确保在删除给定的上下文之后，微筛选器驱动程序不会调用 **FltReferenceContext** (参见参数 2) 。

 

 




