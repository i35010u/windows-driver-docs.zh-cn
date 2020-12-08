---
title: 锁定 ntsdexts 锁
description: Ntsdexts.dll 中的锁扩展显示与当前进程相关联的关键部分的列表。不应将此扩展命令与 kdext *. 锁 extension 命令混淆。
keywords:
- ) Windows 调试中锁定 ( ntsdexts
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- locks ( ntsdexts.locks)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eefa371f4ec09d080b9bd4b093cc19a1798d4998
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829813"
---
# <a name="locks-ntsdextslocks"></a>!locks (!ntsdexts.locks)


Ntsdexts.dll 中的 **！锁** 扩展显示与当前进程相关联的关键部分的列表。

此扩展命令不应与 [**！ kdext \* extension**](-locks---kdext--locks-.md) 命令混淆。

```dbgcmd
    !locks [Options] 
```

## <a name="span-idddk__ntsdexts_locks_dbgspanspan-idddk__ntsdexts_locks_dbgspanparameters"></a><span id="ddk__ntsdexts_locks_dbg"></span><span id="DDK__NTSDEXTS_LOCKS_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
指定要显示的信息量。 可以使用下列选项的任意组合：

<span id="-v"></span><span id="-V"></span>**-v**  
使显示内容包括所有关键部分，甚至包括当前不拥有的部分。

<span id="-o"></span><span id="-O"></span>**-o**  
使显示仅包含孤立信息 (指针，这些指针实际上不会指向有效的关键部分) 。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关可显示关键部分信息的其他命令和扩展，请参阅 [显示关键部分](displaying-a-critical-section.md)。 有关关键部分的信息，请参阅 Microsoft Windows SDK 文档、Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部机制* ，并将标记 Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

此扩展命令显示已通过调用 **RtlInitializeCriticalSection** 初始化的所有关键部分。 如果没有关键部分，则不会产生任何输出。

以下是示例：

```dbgcmd
0:000> !locks

CritSec w3svc!g_pWamDictator+a0 at 68C2C298
LockCount          0
RecursionCount     1
OwningThread       d1
EntryCount         1
ContentionCount    0
**_ Locked

CritSec SMTPSVC+66a30 at 67906A30
LockCount          0
RecursionCount     1
OwningThread       d0
EntryCount         1
ContentionCount    0
_** Locked
```

 

 





