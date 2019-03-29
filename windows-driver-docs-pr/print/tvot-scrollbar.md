---
title: TVOT\_滚动条
description: TVOT\_滚动条
ms.assetid: 8d905933-9629-48eb-9130-afa3dfa15099
keywords:
- TVOT_SCROLLBAR 打印设备
topic_type:
- apiref
api_name:
- TVOT_SCROLLBAR
api_location:
- compstui.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f61b413adeb72bdfcb89c50d9a510d7d49e5024
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566908"
---
# <a name="tvotscrollbar"></a>TVOT\_滚动条


## <span id="ddk_tvot_scrollbar_gg"></span><span id="DDK_TVOT_SCROLLBAR_GG"></span>


TVOT\_包含组框中的滚动条的滚动条选项类型。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM** ](https://msdn.microsoft.com/library/windows/hardware/ff559656)结构  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
值，该值表示当前滚动条的位置。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM** ](https://msdn.microsoft.com/library/windows/hardware/ff559660)结构数组 (**pOptParam**的成员[ **OPTTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff559670))  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
**pOptParam**\[0\]-&gt;**pData**指向标识滚动栏单位的以 NULL 结尾的文本字符串。

**pOptParam**\[1\]-&gt;**pData**指向描述滚动条范围的低端的以 NULL 结尾的文本字符串。

**pOptParam**\[2\]-&gt;**pData**到 aNULL 终止文本字符串，描述滚动条范围的高端点。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
**pOptParam**\[0\]-&gt;**IconID**标识要与滚动条相关联的图标。

**pOptParam**\[1\]-&gt;**IconID**指定表示滚动条范围的低端的 16 位有符号的值。

**pOptParam**\[2\]-&gt;**IconID**指定 mulitplication 的因子，显示其值之前应用于所选的滚动位置。 （通常情况下，此值为 1。）

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
**pOptParam**\[0\]-&gt;**lParam**不使用。

**pOptParam**\[1\]-&gt;**lParam**指定表示滚动条范围的高端的 16 位有符号的值。

**pOptParam**\[2\]-&gt;**lParam**指定滚动的增量值。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff559670)结构  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**Type**  
TVOT\_滚动条

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**Count**  
3

<span id="Style"></span><span id="style"></span><span id="STYLE"></span>**Style**  
不使用。

<span id="BegCtrlID"></span><span id="begctrlid"></span><span id="BEGCTRLID"></span>**BegCtrlID**  
如果**pDlgPage**中[ **COMPROPSHEETUI** ](https://msdn.microsoft.com/library/windows/hardware/ff546211)标识 CPSUI 提供的页，或者如果**DlgTemplateID**中[ **DLGPAGE** ](https://msdn.microsoft.com/library/windows/hardware/ff547607)标识 CPSUI 提供模板**BegCtrlID**不使用。

否则为**BegCtrlID**必须包含一组按顺序编号的控件标识符的第一个控件标识符。 控件标识符必须标识以下 Windows 控件：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>控件标识符</th>
<th>Windows 控件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容</p></td>
<td><p>分组框</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 1</p></td>
<td><p>标题文本</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 2</p></td>
<td><p>滚动条</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容加上 3</p></td>
<td><p>滚动栏图标</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 4</p></td>
<td><p>描述的滚动条范围低端的文本</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 5</p></td>
<td><p>描述滚动条范围的高端的文本</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 6</p></td>
<td><p>描述滚动栏单位的文本</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 7</p></td>
<td><p>扩展的复选框或扩展下压按钮 （可选）</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 8</p></td>
<td><p>扩展的复选框或扩展下压按钮图标 （可选）</p></td>
</tr>
</tbody>
</table>

 

有关其他信息，请参阅[Customizing CPSUI-Supported 窗口控件](https://msdn.microsoft.com/library/windows/hardware/ff547296)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Compstui.h （包括 Compstui.h）</td>
</tr>
</tbody>
</table>

 

 




