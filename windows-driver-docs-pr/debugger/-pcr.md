---
title: pcr
description: Pcr 扩展特定处理器上显示的当前状态的处理器控件区域 (PCR)。
ms.assetid: a9d82aa4-57de-4170-80fd-b7cd5b82f1e5
keywords:
- 处理器控件区域 (PCR)
- pcr Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pcr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 018741ae2a8f28b7b29c55ca10b00f6564a5c5f5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334408"
---
# <a name="pcr"></a>!pcr


**！ Pcr**扩展特定处理器上显示的当前状态的处理器控件区域 (PCR)。

```dbgcmd
!pcr [Processor]
```

## <a name="span-idddkpcrdbgspanspan-idddkpcrdbgspanparameters"></a><span id="ddk__pcr_dbg"></span><span id="DDK__PCR_DBG"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *Processor*   
指定要检索的 PCR 信息的处理器。 如果*处理器*是省略，使用当前的处理器。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>



### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

PCR 和 PRCB 有关的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。

<a name="remarks"></a>备注
-------

处理器控制块 (PRCB) 是 PCR 的扩展。 可以使用显示[ **！ prcb** ](-prcb.md)扩展。

下面是举例 **！ pcr**扩展 x86 目标计算机：

```dbgcmd
kd> !pcr 0
KPCR for Processor 0 at ffdff000:
    Major 1 Minor 1
      NtTib.ExceptionList: 801626e0
          NtTib.StackBase: 801628f0
         NtTib.StackLimit: 8015fb00
       NtTib.SubSystemTib: 00000000
            NtTib.Version: 00000000
        NtTib.UserPointer: 00000000
            NtTib.SelfTib: 00000000

                  SelfPcr: ffdff000
                     Prcb: ffdff120
                     Irql: 00000000
                      IRR: 00000000
                      IDR: ffffffff
            InterruptMode: 00000000
                      IDT: 80043400
                      GDT: 80043000
                      TSS: 803cc000

            CurrentThread: 8015e8a0
               NextThread: 00000000
               IdleThread: 8015e8a0

                DpcQueue:  0x80168ee0 0x80100d04 ntoskrnl!KiTimerExpiration
```

在此显示中的条目之一显示中断请求级别 (IRQL)。 **！ Pcr**扩展会显示当前 IRQL，但当前 IRQL 通常并不是更感兴趣。 已存在的 bug 检查或调试器连接之前，只需 IRQL 是更有趣。 此情况下将显示[ **！ irql**](-irql.md)，这只是运行 Windows Server 2003 或更高版本的 Windows 计算机上可用。









