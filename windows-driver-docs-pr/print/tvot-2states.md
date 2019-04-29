---
title: TVOT\_2STATES
description: TVOT\_2STATES
ms.assetid: e8d89cf6-275d-4a2a-8a8e-8799988c31e2
keywords:
- TVOT_2STATES 打印设备
topic_type:
- apiref
api_name:
- TVOT_2STATES
api_location:
- compstui.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c91170c148ee26d7b32216f974508b6102c73b26
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364933"
---
# <a name="tvot2states"></a>TVOT\_2STATES


## <span id="ddk_tvot_2states_gg"></span><span id="DDK_TVOT_2STATES_GG"></span>


TVOT\_2STATES 选项类型包含组框中的两个单选按钮。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM** ](https://msdn.microsoft.com/library/windows/hardware/ff559656)结构  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
中的索引[ **OPTPARAM** ](https://msdn.microsoft.com/library/windows/hardware/ff559660)所指向的数组**pOptParam**成员的选项[ **OPTTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff559670)结构。 这将指定当前所选的选项参数。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM** ](https://msdn.microsoft.com/library/windows/hardware/ff559660)结构数组 (**pOptParam**的成员[ **OPTTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff559670))  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
**pOptParam**\[0\]-&gt;**pData**指向描述状态 1，用作按钮标签的文本字符串。

**pOptParam**\[1\]-&gt;**pData**指向描述状态 2，用作按钮标签的文本字符串。

如果两个状态为 OFF/ON、 FALSE/TRUE，否 / 是，依次类推，state 1 必须为 OFF、 FALSE 或未启用状态。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
**pOptParam**\[0\]-&gt;**IconID**标识要与状态 1 相关联的图标。

**pOptParam**\[1\]-&gt;**IconID**标识要与状态 2 相关联的图标。

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
不使用。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff559670)结构  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**Type**  
TVOT\_2STATES

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**Count**  
2

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
<td><p>状态 1 单选按钮</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容加上 3</p></td>
<td><p>状态 1 图标</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 4</p></td>
<td><p>状态 2 单选按钮</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 5</p></td>
<td><p>状态 2 图标</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 6</p></td>
<td><p>扩展的复选框或扩展下压按钮 （可选）</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 7</p></td>
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

 

 




