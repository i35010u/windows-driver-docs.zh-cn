---
title: 僵停
description: 僵尸扩展显示所有死 ( "傀儡" ) 进程或线程。
keywords:
- 僵尸 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- zombies
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c5244b96b277d6583bb73d94ab183f368cc12eeb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808527"
---
# <a name="zombies"></a>!zombies


**！僵尸** 扩展显示所有死 ( "傀儡" ) 进程或线程。

```dbgcmd
!zombies [Flags [RestartAddress]]
```

## <a name="span-idddk__zombies_dbgspanspan-idddk__zombies_dbgspanparameters"></a><span id="ddk__zombies_dbg"></span><span id="DDK__ZOMBIES_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定将显示的内容。 可能的值包括：

<span id="1"></span>1  
显示所有僵停进程。  (这是默认值。 ) 

<span id="2"></span>2  
显示所有僵停的线程。

<span id="_______RestartAddress______"></span><span id="_______restartaddress______"></span><span id="_______RESTARTADDRESS______"></span>*RestartAddress*   
指定从其开始搜索的十六进制地址。 如果以前的搜索提前终止，这会很有用。 默认值为零。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

若要查看所有进程和线程的列表，请使用 [**！进程**](-process.md) 扩展。

有关内核模式下的进程和线程的一般信息，请参阅 [更改上下文](changing-contexts.md)。 有关分析进程和线程的详细信息，请参阅 Russinovich 和 David 所罗门群岛的 *Microsoft Windows 内部机制*。 

<a name="remarks"></a>备注
-------

僵停进程是尚未从进程列表中删除的停滞进程。 僵停线程类似。

此扩展仅适用于 Windows 2000。

 

 





