---
title: TVOT\_TRACKBAR
description: TVOT\_TRACKBAR
ms.assetid: 00140dca-c192-42dc-853d-ae84c602b206
keywords:
- TVOT_TRACKBAR 打印设备
topic_type:
- apiref
api_name:
- TVOT_TRACKBAR
api_location:
- compstui.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a03d1724d729181f46d128fa3d944f38211b494
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378601"
---
# <a name="tvottrackbar"></a>TVOT\_TRACKBAR


## <span id="ddk_tvot_trackbar_gg"></span><span id="DDK_TVOT_TRACKBAR_GG"></span>


TVOT\_包含组框中的跟踪条的跟踪条选项类型。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_optitem)结构  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
值，该值表示当前的跟踪条位置。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_optparam)结构数组 (**pOptParam**的成员[ **OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_opttype))  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
**pOptParam**\[0\]-&gt;**pData**指向标识跟踪栏单位的以 NULL 结尾的文本字符串。

**pOptParam**\[1\]-&gt;**pData**指向描述跟踪条范围的低端的以 NULL 结尾的文本字符串。

**pOptParam**\[2\]-&gt;**pData**指向描述跟踪条范围的高端的以 NULL 结尾的文本字符串。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
**pOptParam**\[0\]-&gt;**IconID**标识要与跟踪条相关联的图标。

**pOptParam**\[1\]-&gt;**IconID**指定表示跟踪条范围的低端的 16 位有符号的值。

**pOptParam**\[2\]-&gt;**IconID**指定应用于它的值显示所选的跟踪位置 gefore 的乘法因子。 （通常情况下，此值为 1。）

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
**pOptParam**\[0\]-&gt;**lParam**不使用。

**pOptParam**\[1\]-&gt;**lParam**指定表示跟踪条范围的高端的 16 位有符号的值。

**pOptParam**\[2\]-&gt;**lParam**指定跟踪增量值。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_opttype)结构  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**Type**  
TVOT\_TRACKBAR

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**Count**  
3

<span id="Style"></span><span id="style"></span><span id="STYLE"></span>**Style**  
不使用。

<span id="BegCtrlID"></span><span id="begctrlid"></span><span id="BEGCTRLID"></span>**BegCtrlID**  
如果**pDlgPage**中[ **COMPROPSHEETUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_compropsheetui)标识 CPSUI 提供的页，或者如果**DlgTemplateID**中[ **DLGPAGE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_dlgpage)标识 CPSUI 提供模板**BegCtrlID**不使用。

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
<td><p>跟踪条</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容加上 3</p></td>
<td><p>跟踪栏图标</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 4</p></td>
<td><p>描述跟踪条范围低端的文本</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 5</p></td>
<td><p>描述跟踪条范围的高端的文本</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 6</p></td>
<td><p>描述跟踪栏单位的文本</p></td>
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

 

有关其他信息，请参阅[Customizing CPSUI-Supported 窗口控件](https://docs.microsoft.com/windows-hardware/drivers/print/customizing-cpsui-supported-window-controls)。

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

 

 




