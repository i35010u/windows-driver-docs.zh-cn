---
title: TVOT\_COMBOBOX
description: TVOT\_COMBOBOX
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
ms.openlocfilehash: dfb6caebe89735240e3ebef141678c5a10a152d1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845256"
---
# <a name="tvot_combobox"></a>TVOT\_COMBOBOX


## <span id="ddk_tvot_combobox_gg"></span><span id="DDK_TVOT_COMBOBOX_GG"></span>


TVOT\_COMBOBOX 选项类型由组合框中的组合框组成。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem)构造  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
[**OPTPARAM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam)数组中的索引，该数组由该选项的[**OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)结构的**pOptParam**成员指向。 这会指定当前选择的选项参数。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam)结构数组（ [**OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)的**pOptParam**成员）  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
**pOptParam**\[0\]-&gt;**pData**指向要在组合框中显示的第一个文本字符串。

**pOptParam**\[1\]-&gt;**pData**指向要在组合框中显示的第二个文本字符串。

**pOptParam**\[*n*\]-&gt;**pData**指向要在组合框中显示的第*n*个文本字符串。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
**pOptParam**\[0\]-&gt;**IconID**标识与第一个文本字符串关联的图标。

**pOptParam**\[1\]-&gt;**IconID**标识与第二个文本字符串关联的图标。

**pOptParam**\[*n*\]-&gt;**IconID**标识与第*n*个文本字符串关联的图标。

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
不使用。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)构造  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**类别**  
TVOT\_COMBOBOX

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**计**  
OPTPARAM 结构的数量;即要在组合框中显示的文本字符串的数目。

<span id="Style"></span><span id="style"></span><span id="STYLE"></span>**方式**  
可以指定以下可选的位标志。

<span id="OTS_LBCB_INCL_ITEM_NONE"></span><span id="ots_lbcb_incl_item_none"></span>OTS\_LBCB\_包括\_项\_NONE  
如果设置，CPSUI 在组合框中包含 "None" 字符串。 如果用户选择 "无"，则**Sel/pSel** union 设置为负一。

<span id="OTS_LBCB_NO_ICON16_IN_ITEM"></span><span id="ots_lbcb_no_icon16_in_item"></span>OTS\_LBCB\_\_项中没有\_ICON16\_  
如果设置此参数，则在组合框中显示参数的值时，CPSUI 不会绘制每个选项参数的图标（OPTPARAM 中的**IconID** ）。

<span id="OTS_LBCB_PROPPAGE_CBUSELB"></span><span id="ots_lbcb_proppage_cbuselb"></span>OTS\_LBCB\_属性页\_CBUSELB  
当选项显示在 nontreeview 属性表页上时，它将显示为 listbox 而不是 combobox。

<span id="OTS_LBCB_SORT"></span><span id="ots_lbcb_sort"></span>OTS\_LBCB\_排序  
如果设置，CPSUI 按字母顺序显示文本字符串。

<span id="BegCtrlID"></span><span id="begctrlid"></span><span id="BEGCTRLID"></span>**BegCtrlID**  
如果[**COMPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_compropsheetui)中的**pDlgPage**标识 CPSUI 提供的页面，或[**DLGPAGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_dlgpage)中的**DlgTemplateID**标识 CPSUI 提供的模板，则不使用**BegCtrlID** 。

否则， **BegCtrlID**必须包含按顺序编号的控件标识符集的第一个控件标识符。 控件标识符必须标识以下 Windows 控件：

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
<td><p><strong>BegCtrlID</strong>内容 + 3</p></td>
<td><p>组合框图标</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 4</p></td>
<td><p>"扩展" 复选框或扩展的 "推送" 按钮（可选）</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 5</p></td>
<td><p>"扩展" 复选框或 "扩展" 推送按钮图标（可选）</p></td>
</tr>
</tbody>
</table>

 

有关其他信息，请参阅[自定义 CPSUI 支持的窗口控件](https://docs.microsoft.com/windows-hardware/drivers/print/customizing-cpsui-supported-window-controls)。

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
<td>Compstui （包括 Compstui）</td>
</tr>
</tbody>
</table>

 

 




