---
title: 锁 ntsdexts.locks
description: Ntsdexts.dll 中的锁扩展显示与当前进程关联的关键部分的列表。此扩展命令不应与 kdext*.locks 扩展命令混淆。
ms.assetid: f33a68e8-1ddc-4d49-bb22-8f8b097c8ada
keywords:
- 锁 (ntsdexts.locks) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- locks ( ntsdexts.locks)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5947ac71adbfde2a2a85e7fee0adcf05bd69145a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336184"
---
# <a name="locks-ntsdextslocks"></a>!locks (!ntsdexts.locks)


**！ 锁**Ntsdexts.dll 中的扩展显示与当前进程关联的关键部分的列表。

不要将此扩展命令与相混淆[ **！ kdext\*.locks** ](-locks---kdext--locks-.md)扩展命令。

```dbgcmd
    !locks [Options] 
```

## <a name="span-idddkntsdextslocksdbgspanspan-idddkntsdextslocksdbgspanparameters"></a><span id="ddk__ntsdexts_locks_dbg"></span><span id="DDK__NTSDEXTS_LOCKS_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
指定要显示的信息。 可以使用以下选项的任意组合：

<span id="-v"></span><span id="-V"></span>**-v**  
将导致显示效果以包含所有关键部分，甚至包括那些不当前拥有。

<span id="-o"></span><span id="-O"></span>**-o**  
将导致显示效果以仅包括孤立的信息 （实际上不指向有效的关键部分的指针）。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关其他命令和扩展，可以显示关键部分的信息，请参阅[显示关键节](displaying-a-critical-section.md)。 有关关键部分的信息，请参阅 Microsoft Windows SDK 文档，Windows Driver Kit (WDK) 文档，并*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。

<a name="remarks"></a>备注
-------

此扩展命令显示所有已通过调用来初始化的关键部分**RtlInitializeCriticalSection**。 如果不包括任何关键部分，则会不产生任何输出。

下面是一个示例：

```dbgcmd
0:000> !locks

CritSec w3svc!g_pWamDictator+a0 at 68C2C298
LockCount          0
RecursionCount     1
OwningThread       d1
EntryCount         1
ContentionCount    0
*** Locked

CritSec SMTPSVC+66a30 at 67906A30
LockCount          0
RecursionCount     1
OwningThread       d0
EntryCount         1
ContentionCount    0
*** Locked
```

 

 





