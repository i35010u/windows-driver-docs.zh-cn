---
title: TVOT \_ 滚动条
description: TVOT \_ 滚动条
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
ms.openlocfilehash: a648e01f5497d16fb5efb36ecdde1b9ace61c6e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819977"
---
# <a name="tvot_scrollbar"></a>TVOT \_ 滚动条


## <span id="ddk_tvot_scrollbar_gg"></span><span id="DDK_TVOT_SCROLLBAR_GG"></span>


TVOT \_ 滚动条选项类型包括分组框中的滚动条。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem) 构造  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
表示当前滚动条位置的值。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam)结构数组 ([**OPTTYPE**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)的 **pOptParam** 成员)   

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
**pOptParam** \[0 \] - &gt; **pData** 指向以 NULL 结尾的文本字符串，该字符串标识滚动条单位。

**pOptParam** \[1 \] - &gt; **pData** 指向以 NULL 结尾的文本字符串，该字符串描述滚动条范围的下限。

**pOptParam** \[2 \] - &gt; **pData** 指向 aNULL 结束的文本字符串，该字符串描述滚动条范围的上限。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
**pOptParam** \[0 \] - &gt; **IconID** 标识要与滚动条关联的图标。

**pOptParam** \[1 \] - &gt; **IconID** 指定一个16位有符号值，该值表示滚动条范围的下限。

**pOptParam** \[2 \] - &gt; **IconID** 指定在显示其值之前应用于所选滚动位置的 mulitplication 系数。  (通常情况下，此值为1。 ) 

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
**pOptParam** \[0 \] - &gt; **lParam** 不使用。

**pOptParam** \[1 \] - &gt; **lParam** 指定一个16位有符号值，该值表示滚动条范围的上限。

**pOptParam** \[2 \] - &gt; **lParam** 指定滚动增量值。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype) 构造  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**类别**  
TVOT \_ 滚动条

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
<td><p>滚动条</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong> 内容 + 3</p></td>
<td><p>滚动条图标</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong> 内容 + 4</p></td>
<td><p>描述滚动条范围低端的文本</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong> 内容 + 5</p></td>
<td><p>描述滚动条范围的上限的文本</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong> 内容 + 6</p></td>
<td><p>描述滚动条单位的文本</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong> 内容 + 7</p></td>
<td><p>"扩展" 复选框或 "扩展" 推送按钮 (可选) </p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong> 内容 + 8</p></td>
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

 

