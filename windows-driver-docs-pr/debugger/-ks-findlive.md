---
title: ks. findlive
description: Findlive 扩展搜索内部 Ks.sys 调试日志以尝试查找指定类型的活动对象。
keywords:
- findlive Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.findlive
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 06c90100a81141ed926a722b80af3b3f8e535630
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828287"
---
# <a name="ksfindlive"></a>!ks.findlive


**！ Findlive** extension 搜索内部 Ks.sys 调试日志，以尝试查找指定类型的活动对象。

```dbgcmd
!ks.findlive Type [Entries] [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span>*类型*   
指定要搜索的对象的类型。 输入以下内容之一作为文本值： **Queue**、 **请求** 者、 **Pin**、 **筛选器** 或 **Irp**。

<span id="Entries"></span><span id="entries"></span><span id="ENTRIES"></span>日志  
如果此参数为零或省略，则搜索整个日志。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span>*级别*   
可选。 指定要在0-7 刻度上显示的详细信息的级别，并为较高的值显示更多的信息。 若要显示所有可用的详细信息，请提供值7。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核流调试](kernel-streaming-debugging.md)。

<a name="remarks"></a>备注
-------

**！ Findlive** 命令可能找不到所有可能的指定活动对象。

此扩展要求目标计算机运行 Ks.sys 的已选中 (调试) 版本。

 

 





