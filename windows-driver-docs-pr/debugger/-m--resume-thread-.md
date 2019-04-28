---
title: ~m（恢复线程）
description: ~ M 命令恢复指定线程的执行。不要混淆此命令使用 m （移动内存） 命令。
ms.assetid: fc4eec45-2a28-4571-abf5-3896b77a52c9
keywords:
- ~ m （恢复线程） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~m (Resume Thread)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f783fe1bc23252fbc40d936124711d8b2ccd0d3f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336098"
---
# <a name="m-resume-thread"></a>~m（恢复线程）


**~ M**命令恢复指定线程的执行。

不要将使用此命令相混淆[ **m （移动内存）** ](m--move-memory-.md)命令。

```dbgcmd
~Thread m 
```

## <a name="span-idddkcmdresumethreaddbgspanspan-idddkcmdresumethreaddbgspanparameters"></a><span id="ddk_cmd_resume_thread_dbg"></span><span id="DDK_CMD_RESUME_THREAD_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定的线程或线程继续。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>仅限用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关挂起计数和如何挂起的线程的行为并控制挂起和冻结的线程的其他命令的列表，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

仅在用户模式下，可以指定线程。 在内核模式下颚化符 （~） 是指一个处理器。

使用每次 **~ m**命令时，线程的挂起计数减少 1。

 

 





