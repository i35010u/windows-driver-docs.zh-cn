---
title: .ttime （显示线程时间）
description: .Ttime 命令显示线程正在运行的时间。
ms.assetid: ff48310f-3eb9-4112-b5ab-b7c16878ac8f
keywords:
- .ttime （显示线程时间） Windows 调试
ms.date: 08/01/2018
topic_type:
- apiref
api_name:
- .ttime (Display Thread Times)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 49fd367035c7fb38f99c1c30782701d211fd0f36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544346"
---
# <a name="ttime-display-thread-times"></a>.ttime （显示线程时间）


**.Ttime**命令显示线程正在运行的时间。

```dbgcmd
.ttime 
```

## <span id="ddk_meta_display_thread_times_dbg"></span><span id="DDK_META_DISPLAY_THREAD_TIMES_DBG"></span>


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
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>仅限 x86</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此命令仅适用于用户模式。 在内核模式下应使用[ **！ 线程**](-thread.md)相反。 只要用户创建后，此命令适用于用户模式的小型转储 **/mt**或 **/ma**选项，请参见[用户模式转储文件](user-mode-dump-files.md)有关详细信息。

**.Ttime**命令显示了线程，以及在内核模式下和在用户模式下运行的时间量的创建时间。

下面是一个示例：

```dbgcmd
0:000> .ttime
Created: Sat Jun 28 17:58:42 2003
Kernel:  0 days 0:00:00.131
User:    0 days 0:00:02.109
```

 

 





