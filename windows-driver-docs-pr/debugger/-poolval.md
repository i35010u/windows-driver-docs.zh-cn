---
title: poolval
description: Poolval 扩展分析分页池的标头，并诊断任何可能已损坏。 此扩展是仅在 Windows XP 和更高版本中可用。
ms.assetid: b67ab2d4-c765-4721-81ed-c6b7c9a0ba6d
keywords:
- poolval Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- poolval
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3874c69e83ea9c6a3c9e5bdfdd3fa1e0d015ce52
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543038"
---
# <a name="poolval"></a>！ poolval


**！ Poolval**扩展分析分页池的标头并诊断任何可能已损坏。 此扩展是仅在 Windows XP 和更高版本中可用。

```dbgcmd
!poolval Address [DisplayLevel]
```

## <a name="span-idddkpoolvaldbgspanspan-idddkpoolvaldbgspanparameters"></a><span id="ddk__poolval_dbg"></span><span id="DDK__POOLVAL_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要对其进行分析的标头的池的地址。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span> *DisplayLevel*   
指定要包括在显示的信息。 这可以是任何以下值 （默认值为零）：

<span id="0"></span>0  
导致要显示的基本信息。

<span id="1"></span>1  
要显示的原因的基本信息和链接标头列表。

<span id="2"></span>2  
会导致基本信息、 链接标头列表和要显示的基本标头信息。

<span id="3"></span>3  
会导致基本信息、 链接标头列表和要显示的完整的标头信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关内存池的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 （这些资源可能不可用在某些语言和国家/地区中。）

 

 





