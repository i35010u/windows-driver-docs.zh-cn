---
title: ~ s （更改当前处理器）
description: ~ S 命令设置的多处理器系统上调试哪个处理器。在内核模式下，~ s 更改当前的处理器。
ms.assetid: bd036a25-1e3c-4b57-9c7c-5f1730008cd7
keywords:
- 更改当前处理器 (~ s) 命令
- 多处理器计算机，更改当前处理器 (~ s) 命令
- 处理器
- ~ s （更改当前处理器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~s (Change Current Processor)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 30b4e8cc1a59cfb25f6485536b4d88b8bc146b75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546424"
---
# <a name="s-change-current-processor"></a>~ s （更改当前处理器）


**~ S**命令设置的多处理器系统上调试哪个处理器。

在内核模式下 **~ s**更改当前的处理器。 不要将使用此命令相混淆[ **~ （设置当前线程） s** ](-s--set-current-thread-.md)命令 （仅在用户模式下的工作方式）， [ **| s （设置当前进程）** ](-s--set-current-process-.md)命令， [ **| |s （设置当前系统）** ](--s--set-current-system-.md)命令，或[ **s （内存搜索）** ](s--search-memory-.md)命令。

```dbgcmd
~Processor s
```

## <a name="span-idddkcmdchangecurrentprocessordbgspanspan-idddkcmdchangecurrentprocessordbgspanparameters"></a><span id="ddk_cmd_change_current_processor_dbg"></span><span id="DDK_CMD_CHANGE_CURRENT_PROCESSOR_DBG"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *Processor*   
指定要调试的处理器数。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

仅在内核模式下，可以指定处理器。 在用户模式下，颚化符 （~） 是指一个线程。

可以立即确定您在处理多个处理器系统上的内核调试提示形状情况。 在下面的示例中，0： 意味着你调试的计算机中的第一个处理器。

```dbgcmd
0: kd>
```

使用以下命令处理器之间切换：

```dbgcmd
0: kd> ~1s
1: kd>
```

现在正在调试的计算机的第二个处理器。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[多处理器语法](multiprocessor-syntax.md)

 

 






