---
title: ~m（恢复线程）
description: ~ M 命令恢复指定线程的执行。请勿将此命令与 m (移动内存) 命令混淆。
keywords:
- ~ m (恢复线程) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~m (Resume Thread)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7f2b24430cefe1754f9f3cbf1f27ad8eebdf79c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815241"
---
# <a name="m-resume-thread"></a>~m（恢复线程）


**~ M** 命令恢复指定线程的执行。

请勿将此命令与 [**m (移动内存)**](m--move-memory-.md) 命令混淆。

```dbgcmd
~Thread m 
```

## <a name="span-idddk_cmd_resume_thread_dbgspanspan-idddk_cmd_resume_thread_dbgspanparameters"></a><span id="ddk_cmd_resume_thread_dbg"></span><span id="DDK_CMD_RESUME_THREAD_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
指定要恢复的一个或一线程。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

若要详细了解暂停计数和挂起线程的行为方式，以及控制挂起和冻结线程的其他命令的列表，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

只能在用户模式下指定线程。 在内核模式下，颚化 (~) 引用处理器。

每次使用 **~ m** 命令时，线程的挂起计数将减少1。

 

 





