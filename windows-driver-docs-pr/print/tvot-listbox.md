---
title: TVOT \_ LISTBOX
description: TVOT \_ LISTBOX
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
ms.openlocfilehash: daaa602b60be5fe86b0108e1b17253e8076f0e9e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792593"
---
# <a name="tvot_listbox"></a>TVOT \_ LISTBOX


## <span id="ddk_tvot_listbox_gg"></span><span id="DDK_TVOT_LISTBOX_GG"></span>


TVOT \_ LISTBOX 选项类型包括分组框中的列表框。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem) 构造  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
[**OPTPARAM**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam)数组中的索引，该数组由该选项的 [**OPTTYPE**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)结构的 **pOptParam** 成员指向。 这会指定当前选择的选项参数。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam)结构数组 ([**OPTTYPE**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)的 **pOptParam** 成员)   

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
**pOptParam** \[0 \] - &gt; **pData** 指向要在列表框中显示的第一个文本字符串。

**pOptParam** \[1 \] - &gt; **pData** 指向要在列表框中显示的第二个文本字符串。

**pOptParam** \[*n* \] - n &gt;**pData** 指向要在列表框中显示的第 *n* 个文本字符串。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
**pOptParam** \[0 \] - &gt; **IconID** 标识要与第一个文本字符串关联的图标。

**pOptParam** \[1 \] - &gt; **IconID** 标识要与第二个文本字符串关联的图标。

**pOptParam** \[*n* \] - n &gt;**IconID** 标识与第 *n* 个文本字符串关联的图标。

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
未使用。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype) 构造  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**类别**  
TVOT \_ LISTBOX

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**计**  
OPTPARAM 结构的数量;也就是说，将在列表框中显示的文本字符串的数目。

<span id="Style"></span><span id="style"></span><span id="STYLE"></span>**方式**  
可以指定以下可选的位标志。

<span id="OTS_LBCB_INCL_ITEM_NONE"></span><span id="ots_lbcb_incl_item_none"></span>OTS \_ LBCB （ \_ 包括 \_ 项 \_ NONE）  
如果设置此属性，CPSUI 将在列表框中包含 "None" 字符串。 如果用户选择 "无"，则 **Sel/pSel** union 设置为负一。

<span id="OTS_LBCB_NO_ICON16_IN_ITEM"></span><span id="ots_lbcb_no_icon16_in_item"></span>OTS \_ LBCB \_ \_ ICON16 \_ \_  
如果设置此参数，则在列表框中显示参数的值时，CPSUI 不会在 OPTPARAM) 中 (**IconID** 绘制每个选项参数的图标。

<span id="OTS_LBCB_PROPPAGE_LBUSECB"></span><span id="ots_lbcb_proppage_lbusecb"></span>OTS \_ LBCB \_ 属性页 \_ LBUSECB  
当选项显示在 nontreeview 属性表页上时，它将显示为组合框而不是列表框。

<span id="OTS_LBCB_SORT"></span><span id="ots_lbcb_sort"></span>OTS \_ LBCB \_ SORT  
如果设置，CPSUI 按字母顺序显示文本字符串。

<span id="BegCtrlID"></span><span id="begctrlid"></span><span id="BEGCTRLID"></span>**BegCtrlID**  
如果 [**COMPROPSHEETUI**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_compropsheetui)中的 **pDlgPage** 标识 CPSUI 提供的页面，或 [**DLGPAGE**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_dlgpage)中的 **DlgTemplateID** 标识 CPSUI 提供的模板，则不使用 **BegCtrlID** 。

否则， **BegCtrlID** 必须包含按顺序编号的控件标识符集的第一个控件标识符。 控件标识符必须标识以下 Windows 控件：

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
<td><p><strong>BegCtrlID</strong> 内容</p></td>
<td><p>分组框</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong> 内容 + 1</p></td>
<td><p>标题文本</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong> 内容 + 2</p></td>
<td><p>列表框</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong> 内容 + 3</p></td>
<td><p>列表框图标</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong> 内容 + 4</p></td>
<td><p>"扩展" 复选框或 "扩展" 推送按钮 (可选) </p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong> 内容 + 5</p></td>
<td><p>"扩展" 复选框或 "扩展" 推送按钮图标 (可选) </p></td>
</tr>
</tbody>
</table>

 

有关其他信息，请参阅 [自定义 CPSUI-Supported 窗口控件](./customizing-cpsui-supported-window-controls.md)。

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
<td>Compstui (包含 Compstui) </td>
</tr>
</tbody>
</table>

 

