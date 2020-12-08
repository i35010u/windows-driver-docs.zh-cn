---
title: .ttime（显示线程时间）
description: Ttime 命令显示线程的运行时间。
keywords:
- ttime (显示线程时间) Windows 调试
ms.date: 08/01/2018
topic_type:
- apiref
api_name:
- .ttime (Display Thread Times)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4549edf30f32849ce69837e9d290aff0a2da1be4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838535"
---
# <a name="ttime-display-thread-times"></a>.ttime（显示线程时间）


**Ttime** 命令显示线程的运行时间。

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
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>仅限 x86</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此命令仅在用户模式下工作。 在内核模式下，应该改用 [**！线程**](-thread.md) 。 此命令适用于用户模式小型转储，前提是它们是使用 **/mt** 或 **/ma** 选项创建的;有关详细信息，请参阅 [用户模式转储文件](user-mode-dump-files.md) 。

**Ttime** 命令显示线程的创建时间以及它在内核模式和用户模式下运行的时间量。

以下是示例：

```dbgcmd
0:000> .ttime
Created: Sat Jun 28 17:58:42 2003
Kernel:  0 days 0:00:00.131
User:    0 days 0:00:02.109
```

 

 





