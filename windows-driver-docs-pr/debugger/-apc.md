---
title: apc
description: Apc 扩展会格式化并显示一个或多个异步过程调用 (Apc) 的内容。
keywords:
- apc Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- apc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8d07e06e497bd7571652278ae81c0ce28320894e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800041"
---
# <a name="apc"></a>!apc


**！ Apc** 扩展格式化并显示一个或多个异步过程调用 (apc) 的内容。

```dbgcmd
    !apc
    !apc proc Process
    !apc thre Thread
    !apc KAPC
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="Process"></span><span id="process"></span><span id="PROCESS"></span>*正在*  
指定要显示其 Apc 的进程的地址。

<span id="Thread"></span><span id="thread"></span><span id="THREAD"></span>*Thread*  
指定要显示其 Apc 的线程的地址。

<span id="_______KAPC______"></span><span id="_______kapc______"></span>*KAPC*   
指定要显示的内核 APC 的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


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

 

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


有关 Apc 的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档和 Microsoft Windows 内部机制，Mark Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

如果没有任何参数， **！ apc** 将显示所有 apc。

以下是示例：

```console
kd> !apc
*** Enumerating APCs in all processes
Process e0000000858ba8b0 System
Process e0000165fff86040 smss.exe
Process e0000165fff8c040 csrss.exe
Process e0000165fff4e1d0 winlogon.exe
Process e0000165fff101d0 services.exe
Process e0000165fffa81d0 lsass.exe
Process e0000165fff201d0 svchost.exe
Process e0000165fff8e040 svchost.exe
Process e0000165fff3e040 svchost.exe
Process e0000165fff6e040 svchost.exe
Process e0000165fff24040 spoolsv.exe
Process e000000085666640 wmiprvse.exe
Process e00000008501e520 wmiprvse.exe
Process e0000000856db480 explorer.exe
Process e0000165fff206a0 ctfmon.exe
Process e0000000850009d0 ctfmon.exe
Process e0000165fff51600 conime.exe
Process e000000085496340 taskmgr.exe
Process e000000085489c30 userinit.exe
```

 

 





