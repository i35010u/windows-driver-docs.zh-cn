---
title: TVOT\_跟踪条
description: TVOT\_跟踪条
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
ms.openlocfilehash: c0aba932e002c27353b4ad1e47a908ccaed43650
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845244"
---
# <a name="tvot_trackbar"></a>TVOT\_跟踪条


## <span id="ddk_tvot_trackbar_gg"></span><span id="DDK_TVOT_TRACKBAR_GG"></span>


TVOT\_跟踪条选项类型包括分组框内的跟踪条。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem)构造  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
表示当前跟踪条位置的值。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam)结构数组（ [**OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)的**pOptParam**成员）  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
**pOptParam**\[0\]-&gt;**PDATA**指向以 NULL 结尾的文本字符串，该字符串标识跟踪条单位。

**pOptParam**\[1\]-&gt;**PDATA**指向以 NULL 结尾的文本字符串，该字符串描述跟踪条范围的下限。

**pOptParam**\[2\]-&gt;**PDATA**指向以 NULL 结尾的文本字符串，该字符串描述跟踪条范围的上限。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
**pOptParam**\[0\]-&gt;**IconID**标识与跟踪条关联的图标。

**pOptParam**\[1\]-&gt;**IconID**指定一个16位有符号值，该值表示跟踪条范围的下限。

**pOptParam**\[2\]-&gt;**IconID**指定应用于所选轨迹位置的乘因数，并显示其值。 （通常情况下，此值为1。）

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
未使用**pOptParam**\[0\]-&gt;**lParam** 。

**pOptParam**\[1\]-&gt;**lParam**指定表示跟踪条范围的上限的16位带符号值。

**pOptParam**\[2\]-&gt;**lParam**指定跟踪增量值。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)构造  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**类别**  
TVOT\_跟踪条

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**计**  
3

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
<td><p>跟踪栏</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 3</p></td>
<td><p>跟踪栏图标</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 4</p></td>
<td><p>描述跟踪条范围下限的文本</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 5</p></td>
<td><p>描述跟踪条范围的上限的文本</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 6</p></td>
<td><p>描述跟踪条单位的文本</p></td>
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

 

 




