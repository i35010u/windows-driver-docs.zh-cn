---
title: gdikdx.verifier
description: Gdikdx.verifier 扩展验证图形驱动程序时显示的驱动程序验证程序的状态。
ms.assetid: a7e189bb-ed63-4da3-ab7a-bf502ec131ed
keywords:
- gdikdx.verifier Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gdikdx.verifier
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0c2d691e8dcf7a6743776c60c3a8bb8646b945a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336568"
---
# <a name="gdikdxverifier"></a>!gdikdx.verifier


**！ Gdikdx.verifier**扩展验证图形驱动程序时显示的驱动程序验证程序的状态。

```dbgcmd
!gdikdx.verifier [-Flags] 
```

## <a name="span-idddkgdikdxverifierdbgspanspan-idddkgdikdxverifierdbgspanparameters"></a><span id="ddk__gdikdx_verifier_dbg"></span><span id="DDK__GDIKDX_VERIFIER_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定将在此命令的输出中显示哪些信息。 允许使用以下 （前面加一个连字符） 的任意组合：

<span id="d"></span><span id="D"></span>**d**  
显示包含在统计信息将导致**内存池跟踪**。 这包括地址、 大小和标记的每个池。

<span id="h__or___"></span><span id="H__OR___"></span>**h** (或 **？**)  
在调试器命令窗口中显示此命令的一些简要帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Gdikdx.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关驱动程序验证程序的信息，请参阅 Windows Driver Kit (WDK) 文档。

<a name="remarks"></a>备注
-------

验证不图形驱动程序，该标准的内核模式下扩展的驱动程序时[ **！ verifier** ](-verifier.md)应使用而不是 **！ gdikdx.verifier**。

无论选择的标志，此扩展将显示处于活动状态的 Driver Verifier 选项。 它将随机故障的频率来显示统计信息。

 

 





