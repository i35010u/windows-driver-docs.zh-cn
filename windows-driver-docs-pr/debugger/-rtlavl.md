---
title: rtlavl
description: Rtlavl 扩展显示 RTL_AVL_TABLE 结构的条目。
keywords:
- avl 表格
- rtlavl Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rtlavl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 90bc2bc3265b62a9300861f06b482f9049524c43
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836901"
---
# <a name="rtlavl"></a>!rtlavl


**！ Rtlavl** EXTENSION 显示 RTL \_ AVL \_ 表结构的条目。

```dbgcmd
!rtlavl Address [Module!Type]
!rtlavl -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定 \_ 要显示的 RTL AVL 表的地址 \_ 。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span>*模块*   
指定在其中定义数据结构的模块。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span>*类型*   
指定数据结构的名称。

<span id="_______-_______"></span> **-?**   
在调试器命令窗口中显示此扩展的一些简短帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

使用 [**！ gentable**](-gentable.md) 扩展显示 AVL 表。

<a name="remarks"></a>备注
-------

包括 <em>模块</em>**！**<em>类型</em> 选项使表中的每个条目都被解释为具有给定的类型。

可以通过在 WinDbg) 中按 CTRL + BREAK (或在 KD 或 CDB) 中按 CTRL + C (，随时中断显示。

 

 





