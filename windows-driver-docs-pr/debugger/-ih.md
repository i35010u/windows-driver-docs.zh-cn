---
title: ih
description: Ih 扩展显示指定处理器的中断历史记录。
keywords:
- 中断历史记录
- ih Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ih
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 73bb3baeadc21afcdff4299a7dd572d94d428088
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788977"
---
# <a name="ih"></a>!ih


**！ Ih** extension 显示指定处理器的中断历史记录。

```dbgcmd
!ih Processor
```

**重要提示**  此命令在 Windows 调试器版本10.0.14257 和更高版本中已弃用，不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*处理器*   
指定处理器。 如果省略了 *processor* ，则使用当前处理器。

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
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

此扩展命令只能与基于 Itanium 的目标计算机一起使用。

<a name="remarks"></a>备注
-------

此扩展显示中断历史记录，而不引用程序计数器符号。 若要使用程序计数器符号显示中断历史记录，请使用 [**！他**](-ihs.md) 的扩展。 若要启用中断历史记录，请将 **/configflag = 32** 添加到启动条目选项。

下面是此扩展的输出示例：

```dbgcmd
kd> !ih
Total # of interruptions = 2093185
Vector              IIP                   IPSR          ExtraField 
 VHPT FAULT  e0000000830d3190      1010092a6018  IFA=      6fc00a0200c 
        VHPT FAULT  e0000000830d33d0      1010092a6018  IFA= 1ffffe00001de2d0 
 VHPT FAULT  e0000000830d33d0      1010092a6018  IFA= 1ffffe01befff338 
        VHPT FAULT  e0000000830d3190      1010092a6018  IFA=      6fc00a0200c 
        VHPT FAULT  e0000000830d33d0      1010092a6018  IFA= 1ffffe00001d9188 
        VHPT FAULT  e0000000830d3880      1010092a6018  IFA= 1ffffe01befff250 
        VHPT FAULT  e0000000830d3fb0      1010092a6018  IFA= e0000165f82dc1c0 
 VHPT FAULT  e000000083063390      1010092a6018  IFA= e0000000fffe0018 
     THREAD SWITCH  e000000085896040  e00000008588c040  OSP= e0000165f82dbd40 
        VHPT FAULT  e00000008329b130      1210092a6018  IFA= e0000165f7edaf30 
        VHPT FAULT  e0000165f7eda640      1210092a6018  IFA= e0000165fff968a9 
    PROCESS SWITCH  e0000000818bbe10  e000000085896040  OSP= e0000165f8281de0 
        VHPT FAULT  e00000008307cfc0      1010092a2018  IFA= e00000008189fe50 
EXTERNAL INTERRUPT  e0000000830623b0      1010092a6018  IVR=               d0 
        VHPT FAULT  e00000008314e310      1010092a2018  IFA= e0000165f88203f0 
        VHPT FAULT  e000000083580760      1010092a2018  IFA= e0000000f00ff3fd 
    PROCESS SWITCH  e00000008558c990  e0000000818bbe10  OSP= e00000008189fe20 
        VHPT FAULT  e00000008307cfc0      1010092a2018  IFA= e0000165f02433f0 
        VHPT FAULT          77cfbda0      1013082a6018  IFA=         77cfbda0 
 VHPT FAULT          77cfbdb0      1213082a6018  IFA=      6fbfee0ff98 
   DATA ACCESS BIT          77b8e150      1213082a6018  IFA=         77c16ab8 
        VHPT FAULT          77ed5d60      1013082a6018  IFA=      6fbfffa6048 
   DATA ACCESS BIT          77ed5d60      1213082a6018  IFA=         77c229c0 
 DATA ACCESS BIT          77b8e1b0      1013082a6018  IFA=         77c1c320 
      USER SYSCALL          77cafa40        10082a6018  Num=               42 
 VHPT FAULT  e00000008344dc20      1010092a6018  IFA= e000010600703784 
...
```

 

 





