---
title: TVOT \_ 3STATES
description: TVOT \_ 3STATES
keywords:
- TVOT_3STATES 打印设备
topic_type:
- apiref
api_name:
- TVOT_3STATES
api_location:
- compstui.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b52160d2def83105b3710a97d07ec081e2d66f5a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821825"
---
# <a name="tvot_3states"></a>TVOT \_ 3STATES


## <span id="ddk_tvot_3states_gg"></span><span id="DDK_TVOT_3STATES_GG"></span>


TVOT \_ 3STATES 选项类型包含组框内的三个单选按钮。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem) 构造  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
[**OPTPARAM**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam)数组中的索引，该数组由该选项的 [**OPTTYPE**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)结构的 **pOptParam** 成员指向。 这会指定当前选择的选项参数。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam)结构数组 ([**OPTTYPE**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)的 **pOptParam** 成员)   

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
**pOptParam** \[0 \] - &gt; **pData** 指向说明状态1的文本字符串，该字符串用作按钮标签。

**pOptParam** \[1 \] - &gt; **pData** 指向说明状态2的文本字符串，用作按钮标签。

**pOptParam** \[2 \] - &gt; **pData** 指向说明状态3的文本字符串，用作按钮标签。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
**pOptParam** \[0 \] - &gt; **IconID** 标识要与状态1关联的图标。

**pOptParam** \[1 \] - &gt; **IconID** 标识与状态2关联的图标。

**pOptParam** \[2 \] - &gt; **IconID** 标识与状态3关联的图标。

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
未使用。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype) 构造  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**类别**  
TVOT \_ 3STATES

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**计**  
3

<span id="Style"></span><span id="style"></span><span id="STYLE"></span>**方式**  
未使用。

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
<td><p>状态1单选按钮</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong> 内容 + 3</p></td>
<td><p>状态1图标</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong> 内容 + 4</p></td>
<td><p>状态2单选按钮</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong> 内容 + 5</p></td>
<td><p>状态2图标</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong> 内容 + 6</p></td>
<td><p>状态3单选按钮</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong> 内容 + 7</p></td>
<td><p>状态3图标</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong> 内容 + 8</p></td>
<td><p>"扩展" 复选框或 "扩展" 推送按钮 (可选) </p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong> 内容 + 9</p></td>
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

 

