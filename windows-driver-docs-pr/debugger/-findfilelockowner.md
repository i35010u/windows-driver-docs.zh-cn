---
title: findfilelockowner
description: Findfilelockowner 扩展会尝试通过检查所有线程被阻止的线程查找文件对象锁的所有者。
ms.assetid: 0d6eabf4-e7ac-4536-beab-d3027720efa8
keywords:
- findfilelockowner Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- findfilelockowner
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 331d20203285de5a75eda12d785b5e767c7b9ff2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337119"
---
# <a name="findfilelockowner"></a>!findfilelockowner


**！ Findfilelockowner**扩展会尝试通过检查所有线程的线程受阻的 IopSynchronousServiceTail 断言中并具有文件对象作为参数来查找文件对象锁的所有者。

```dbgcmd
!findfilelockowner [FileObject]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span> *FileObject*   
指定的文件对象的地址。 如果*的文件对象*省略，则该扩展搜索卡在当前进程中的任何线程**IopAcquireFileObjectLock**和检索文件对象地址，从堆栈跟踪。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关文件对象的信息，请参阅 Microsoft Windows SDK 文档，Windows Driver Kit (WDK) 文档，并*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

此扩展在临界区的超时内的文件，正在等待的线程的超时是最有用**IopAcquireFileObjectLock**。 找到有问题的线程后，该扩展将尝试恢复 IRP 所用的请求并显示正在处理 IRP 的驱动程序。

该扩展需要一些时间才能完成，因为它在系统中遍历所有线程的堆栈，直到找到有问题的线程。你可以停止\`随时通过按 CTRL + BREAK （在 WinDbg) 或 CTRL + C （中 KD)。

 

 





