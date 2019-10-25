---
title: TVOT\_UDARROW
description: TVOT\_UDARROW
ms.assetid: c1182cc5-5d82-4db5-8ef2-7d2601499e72
keywords:
- TVOT_UDARROW 打印设备
topic_type:
- apiref
api_name:
- TVOT_UDARROW
api_location:
- compstui.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a4ef8c97db5ccf95b2b81614754559e1b1dfb1e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845242"
---
# <a name="tvot_udarrow"></a>TVOT\_UDARROW


## <span id="ddk_tvot_udarrow_gg"></span><span id="DDK_TVOT_UDARROW_GG"></span>


TVOT\_UDARROW 选项类型由一个下拉控件和一个编辑控件包含在一个分组框中。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem)构造  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
表示编辑控件当前内容的数字值。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam)结构数组（ [**OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)的**pOptParam**成员）  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
**pOptParam**\[0\]-&gt;**PDATA**指向以 NULL 结尾的文本字符串，该字符串标识控件的单位。

**pOptParam**\[1\]-&gt;**PDATA**指向以 NULL 结尾的文本字符串，该字符串描述控件。 （如果**为 NULL**，则 CPSUI 将显示控件的值范围的低端和高端。）

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
**pOptParam**\[0\]-&gt;**IconID**标识与跟踪条关联的图标。

**pOptParam**\[1\]-&gt;**IconID**指定一个16位有符号值，该值表示控件范围的低端。

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
未使用**pOptParam**\[0\]-&gt;**lParam** 。

**pOptParam**\[1\]-&gt;**lParam**指定一个16位有符号值，该值表示控件范围的高端。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)构造  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**类别**  
TVOT\_UDARROW

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**计**  
2

<span id="Style"></span><span id="style"></span><span id="STYLE"></span>**方式**  
不使用。

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
<td><p>编辑框</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 3</p></td>
<td><p>图标</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 4</p></td>
<td><p>描述值单位的文本</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 5</p></td>
<td><p>描述控件的文本</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 6</p></td>
<td><p>Up-down 控件</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 7</p></td>
<td><p>"扩展" 复选框或扩展的 "推送" 按钮（可选）</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 8</p></td>
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

 

 




