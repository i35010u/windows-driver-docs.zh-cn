---
title: 僵停
description: 僵停扩展显示的所有死信 （"僵尸"） 的进程或线程。
ms.assetid: f7fbce79-456a-4643-ad31-8cb2e6449ecf
keywords:
- 僵停 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- zombies
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8643e04580b7c5077bf5457c47d4b6f6ac8af6ed
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239174"
---
# <a name="zombies"></a>!zombies


**！ 僵停**扩展显示的所有死信 （"僵尸"） 的进程或线程。

```dbgcmd
!zombies [Flags [RestartAddress]]
```

## <a name="span-idddkzombiesdbgspanspan-idddkzombiesdbgspanparameters"></a><span id="ddk__zombies_dbg"></span><span id="DDK__ZOMBIES_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定将显示的内容。 可能值的包括：

<span id="1"></span>1  
显示所有僵停进程。 （这是默认值）。

<span id="2"></span>2  
显示僵停的所有线程。

<span id="_______RestartAddress______"></span><span id="_______restartaddress______"></span><span id="_______RESTARTADDRESS______"></span> *RestartAddress*   
指定要开始搜索的十六进制地址。 这是上一次搜索已过早终止的情况下很有用。 默认值为 0。

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
<td align="left"><p>不可用</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

若要查看所有进程和线程的列表，请使用[ **！ 过程**](-process.md)扩展。

关于进程和线程在内核模式下的常规信息，请参阅[更改上下文](changing-contexts.md)。 有关分析进程和线程的详细信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 

<a name="remarks"></a>备注
-------

僵停进程是死的进程，未卸下从进程列表。 僵停线程是类似的。

此扩展是仅适用于 Windows 2000。

 

 





