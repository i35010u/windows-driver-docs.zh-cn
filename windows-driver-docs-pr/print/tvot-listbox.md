---
title: TVOT\_列表框
description: TVOT\_列表框
ms.assetid: 2426ae5a-33e6-4f16-ad49-ff38ea19e392
keywords:
- TVOT_LISTBOX 打印设备
topic_type:
- apiref
api_name:
- TVOT_LISTBOX
api_location:
- compstui.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d232a061d729fd52d781e5357f9a846ef3beba3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543686"
---
# <a name="tvotlistbox"></a>TVOT\_列表框


## <span id="ddk_tvot_listbox_gg"></span><span id="DDK_TVOT_LISTBOX_GG"></span>


TVOT\_LISTBOX 选项类型包含组框中的列表框。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM** ](https://msdn.microsoft.com/library/windows/hardware/ff559656)结构  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
中的索引[ **OPTPARAM** ](https://msdn.microsoft.com/library/windows/hardware/ff559660)所指向的数组**pOptParam**成员的选项[ **OPTTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff559670)结构。 这将指定当前所选的选项参数。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM** ](https://msdn.microsoft.com/library/windows/hardware/ff559660)结构数组 (**pOptParam**的成员[ **OPTTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff559670))  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
**pOptParam**\[0\]-&gt;**pData**指向要在列表框中显示的第一个文本字符串。

**pOptParam**\[1\]-&gt;**pData**指向要在列表框中显示的第二个文本字符串。

**pOptParam**\[*n*\]-&gt;**pData**指向*n*个要显示的文本字符串在列表框中。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
**pOptParam**\[0\]-&gt;**IconID**标识要与第一个文本字符串关联的图标。

**pOptParam**\[1\]-&gt;**IconID**标识要与第二个文本字符串关联的图标。

**pOptParam**\[*n*\]-&gt;**IconID**标识要与之关联的图标*n*个文本字符串。

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
不使用。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff559670)结构  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**Type**  
TVOT\_列表框

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**Count**  
OPTPARAM 结构; 数即，文本的数字字符串列表框中显示。

<span id="Style"></span><span id="style"></span><span id="STYLE"></span>**Style**  
可以指定以下可选的位标志。

<span id="OTS_LBCB_INCL_ITEM_NONE"></span><span id="ots_lbcb_incl_item_none"></span>OTS\_LBCB\_INCL\_ITEM\_NONE  
如果设置，CPSUI 将包括"None"列表框中的字符串。 如果用户选择"None"、 **Sel/pSel**联合设置为 1。

<span id="OTS_LBCB_NO_ICON16_IN_ITEM"></span><span id="ots_lbcb_no_icon16_in_item"></span>OTS\_LBCB\_NO\_ICON16\_IN\_ITEM  
如果设置，CPSUI 不绘制每个选项参数图标 (**IconID** OPTPARAM 中) 在列表框中显示的参数的值。

<span id="OTS_LBCB_PROPPAGE_LBUSECB"></span><span id="ots_lbcb_proppage_lbusecb"></span>OTS\_LBCB\_PROPPAGE\_LBUSECB  
Nontreeview 属性表页上显示的选项，它被显示为组合框而不是列表框。

<span id="OTS_LBCB_SORT"></span><span id="ots_lbcb_sort"></span>OTS\_LBCB\_SORT  
如果集，CPSUI 按字母顺序显示文本字符串。

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
<td><p>列表框</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容加上 3</p></td>
<td><p>列表框图标</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 4</p></td>
<td><p>扩展的复选框或扩展下压按钮 （可选）</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 5</p></td>
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
<td><p>标头</p></td>
<td>Compstui.h （包括 Compstui.h）</td>
</tr>
</tbody>
</table>

 

 




