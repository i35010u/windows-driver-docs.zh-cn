---
title: TVOT\_组合框
description: TVOT\_组合框
ms.assetid: 186acda6-f87c-4e0f-95b8-d76823354cfd
keywords:
- TVOT_COMBOBOX 打印设备
topic_type:
- apiref
api_name:
- TVOT_COMBOBOX
api_location:
- compstui.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad0b13fb6a30ff1078699a3c8febf6faa4bdec5a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362774"
---
# <a name="tvotcombobox"></a>TVOT\_组合框


## <span id="ddk_tvot_combobox_gg"></span><span id="DDK_TVOT_COMBOBOX_GG"></span>


TVOT\_COMBOBOX 选项类型包含组框中的组合框。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_optitem)结构  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
中的索引[ **OPTPARAM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_optparam)所指向的数组**pOptParam**成员的选项[ **OPTTYPE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_opttype)结构。 这将指定当前所选的选项参数。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_optparam)结构数组 (**pOptParam**的成员[ **OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_opttype))  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
**pOptParam**\[0\]-&gt;**pData**指向要在组合框中显示的第一个文本字符串。

**pOptParam**\[1\]-&gt;**pData**指向要在组合框中显示的第二个文本字符串。

**pOptParam**\[*n*\]-&gt;**pData**指向*n*个要显示的文本字符串在组合框中。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
**pOptParam**\[0\]-&gt;**IconID**标识要与第一个文本字符串关联的图标。

**pOptParam**\[1\]-&gt;**IconID**标识要与第二个文本字符串关联的图标。

**pOptParam**\[*n*\]-&gt;**IconID**标识要与之关联的图标*n*个文本字符串。

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
不使用。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_opttype)结构  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**Type**  
TVOT\_组合框

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**Count**  
OPTPARAM 结构; 数即，文本的数字字符串组合框中显示。

<span id="Style"></span><span id="style"></span><span id="STYLE"></span>**Style**  
可以指定以下可选的位标志。

<span id="OTS_LBCB_INCL_ITEM_NONE"></span><span id="ots_lbcb_incl_item_none"></span>OTS\_LBCB\_INCL\_ITEM\_NONE  
如果设置，CPSUI 将包括"None"组合框中的字符串。 如果用户选择"None"、 **Sel/pSel**联合设置为 1。

<span id="OTS_LBCB_NO_ICON16_IN_ITEM"></span><span id="ots_lbcb_no_icon16_in_item"></span>OTS\_LBCB\_NO\_ICON16\_IN\_ITEM  
如果设置，CPSUI 不绘制每个选项参数图标 (**IconID** OPTPARAM 中) 在组合框中显示的参数的值。

<span id="OTS_LBCB_PROPPAGE_CBUSELB"></span><span id="ots_lbcb_proppage_cbuselb"></span>OTS\_LBCB\_PROPPAGE\_CBUSELB  
当 nontreeview 属性表页上显示的选项时，它被显示为一个列表框而不是一个组合框。

<span id="OTS_LBCB_SORT"></span><span id="ots_lbcb_sort"></span>OTS\_LBCB\_SORT  
如果集，CPSUI 按字母顺序显示文本字符串。

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
<td><p>组合框</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容加上 3</p></td>
<td><p>组合框图标</p></td>
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

 

 




