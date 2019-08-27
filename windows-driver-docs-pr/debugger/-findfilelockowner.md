---
title: findfilelockowner
description: Findfilelockowner 扩展通过检查被阻止的线程的所有线程, 尝试查找文件对象锁的所有者。
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
ms.openlocfilehash: 2993e3e7147c9c60fe9300820e98e9c8ac5e9e5a
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025306"
---
# <a name="findfilelockowner"></a>!findfilelockowner


**! Findfilelockowner** extension 通过检查 IopSynchronousServiceTail 断言中阻止的线程的所有线程, 并将文件对象作为参数来尝试查找文件对象锁的所有者。

```dbgcmd
!findfilelockowner [FileObject]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span>*FileObject*   
指定文件对象的地址。 如果省略*FileObject* , 则扩展会搜索当前进程中停滞在**IopAcquireFileObjectLock**中的任何线程, 并从堆栈跟踪中检索文件对象地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p>Kdexts</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关文件对象的信息, 请参阅 "Microsoft Windows SDK 文档"、"Windows 驱动程序工具包 (WDK)" 文档和*Microsoft Windows 内部*的 "标记 Russinovich" 和 "David 所罗门群岛"。

<a name="remarks"></a>备注
-------

此扩展在关键节超时之后最有用, 在这种情况下, 线程在等待**IopAcquireFileObjectLock**内的文件。 找到有问题的线程后, 扩展将尝试恢复用于该请求的 IRP, 并显示正在处理 IRP 的驱动程序。

扩展需要一些时间才能完成, 因为它会遍历系统中的所有线程, 直到找到有问题的线程为止。可以通过按\` ctrl + BREAK (在 WinDbg 中) 或按 ctrl + C (在 KD 中) 随时停止。

 

 





