---
title: TVOT\_PUSHBUTTON
description: TVOT\_PUSHBUTTON
ms.assetid: 47d51066-c1bc-4a84-bc9b-5091100b9f53
keywords:
- TVOT_PUSHBUTTON 打印设备
topic_type:
- apiref
api_name:
- TVOT_PUSHBUTTON
api_location:
- compstui.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 424a61bfc744cd5270e1850c0caff425bc84b100
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362751"
---
# <a name="tvotpushbutton"></a>TVOT\_PUSHBUTTON


## <span id="ddk_tvot_pushbutton_gg"></span><span id="DDK_TVOT_PUSHBUTTON_GG"></span>


TVOT\_按键选项类型包含分组框内的推送按钮。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_optitem)结构  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
取决于**样式**OPTPARAM 的成员结构，按如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>下压按钮样式</th>
<th>Sel/pSel 使用情况</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_CALLBACK</p></td>
<td><p>不使用。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_DLGPROC</p></td>
<td><p>CPSUI 存储对话框过程的返回值。</p></td>
</tr>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_HTCLRADJ</p></td>
<td><p>CPSUI 存储半色调操作的返回值。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_HTSETUP</p></td>
<td><p>CPSUI 存储半色调操作的返回值。</p></td>
</tr>
</tbody>
</table>

 

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_optparam)结构数组 (**pOptParam**的成员[ **OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_opttype))  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
取决于**样式**成员，如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>下压按钮样式</th>
<th>pData 使用情况</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_CALLBACK</p></td>
<td><p>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-_cpsuicallback" data-raw-source="[&lt;strong&gt;_CPSUICALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-_cpsuicallback)"> <strong>_CPSUICALLBACK</strong></a>-类型化函数。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_DLGPROC</p></td>
<td><p>DLGPROC 键入指向对话框过程 （请参阅 Microsoft Windows SDK 文档）。</p></td>
</tr>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_HTCLRADJ</p></td>
<td><p>COLORADJUSTMENT 结构 （Windows SDK 文档中所述） 的指针。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_HTSETUP</p></td>
<td><p>指向<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_devhtadjdata" data-raw-source="[&lt;strong&gt;DEVHTADJDATA&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_devhtadjdata)"> <strong>DEVHTADJDATA</strong> </a>结构。</p></td>
</tr>
</tbody>
</table>

 

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
标识要与推送按钮关联的图标。

<span id="___________lParam__________"></span><span id="___________lparam__________"></span><span id="___________LPARAM__________"></span> lParam   
依赖于样式成员中，按如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>下压按钮样式</th>
<th>lParam 使用情况</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_CALLBACK</p></td>
<td><p>不使用。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_DLGPROC</p></td>
<td><p>对话框资源或句柄 DLGTEMPLATE 结构的资源标识符 （请参阅 Windows SDK 文档）。 取决于 OPTPARAM 结构中的 DPF_USE_HDLGTEMPLATE 标志<strong>标志</strong>成员。</p></td>
</tr>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_HTCLRADJ</p></td>
<td><p>不使用。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_HTSETUP</p></td>
<td><p>不使用。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="___________Style__________"></span><span id="___________style__________"></span><span id="___________STYLE__________"></span> Style</p></td>
<td><p>指定要 CPSUI 当用户单击推送按钮时执行的操作。 可以是以下值之一：</p></td>
</tr>
<tr class="even">
<td><p><span id="PUSHBUTTON_TYPE_CALLBACK"></span><span id="pushbutton_type_callback"></span>PUSHBUTTON_TYPE_CALLBACK</p></td>
<td><p>CPSUI 调用应用程序的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-_cpsuicallback" data-raw-source="[&lt;strong&gt;_CPSUICALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-_cpsuicallback)"> <strong>_CPSUICALLBACK</strong></a>的类型化回调函数来处理与按钮事件<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_cpsuicbparam" data-raw-source="[&lt;strong&gt;CPSUICBPARAM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_cpsuicbparam)"> <strong>CPSUICBPARAM</strong> </a>结构的<strong>原因</strong>成员设置为 CPSUICB_REASON_PUSHBUTTON。 （CPSUI 忽略回调函数的返回值。）</p></td>
</tr>
<tr class="odd">
<td><p><span id="PUSHBUTTON_TYPE_DLGPROC"></span><span id="pushbutton_type_dlgproc"></span>PUSHBUTTON_TYPE_DLGPROC</p></td>
<td><p>应用程序的对话框过程处理按钮的事件。 (有关详细信息，请参阅<strong>备注</strong>部分，了解<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_dlgpage" data-raw-source="[&lt;strong&gt;DLGPAGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_dlgpage)"> <strong>DLGPAGE</strong></a>。)</p>
<p>当函数收到 WM_INITDIALOG 消息，其<em>lParam</em>自变量指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_cpsuicbparam" data-raw-source="[&lt;strong&gt;CPSUICBPARAM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_cpsuicbparam)"> <strong>CPSUICBPARAM</strong> </a>结构<strong>原因</strong>成员设置为 CPSUICB_REASON_DLGPROC。</p></td>
</tr>
<tr class="even">
<td><p><span id="PUSHBUTTON_TYPE_HTCLRADJ"></span><span id="pushbutton_type_htclradj"></span>PUSHBUTTON_TYPE_HTCLRADJ</p></td>
<td><p>CPSUI 显示半色调颜色对话框调整。</p></td>
</tr>
<tr class="odd">
<td><p><span id="PUSHBUTTON_TYPE_HTSETUP"></span><span id="pushbutton_type_htsetup"></span>PUSHBUTTON_TYPE_HTSETUP</p></td>
<td><p>CPSUI 显示设备半色调对话框安装程序。</p></td>
</tr>
</tbody>
</table>

 

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_opttype)结构  

<span id="___________Type__________"></span><span id="___________type__________"></span><span id="___________TYPE__________"></span> Type   
TVOT\_PUSHBUTTON

<span id="___________Count__________"></span><span id="___________count__________"></span><span id="___________COUNT__________"></span> Count   
1

<span id="___________Style__________"></span><span id="___________style__________"></span><span id="___________STYLE__________"></span> Style   
可以指定以下可选的位标志。

<span id="OTS_PUSH_ENABLE_ALWAYS"></span><span id="ots_push_enable_always"></span>OTS\_推送\_启用\_始终为  
如果设置，推送按钮始终会启用，即使用户不能修改属性表页 (即，即使 CPSUIF\_更新\_未设置权限[ **COMPROPSHEETUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_compropsheetui)结构)。

推送按钮的回调函数必须显示其对话框中，但它不能允许用户修改。

注意：您还必须在设置此标志**标志**的成员[ **OPTTYPE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_opttype)结构。

<span id="OTS_PUSH_INCL_SETUP_TITLE"></span><span id="ots_push_incl_setup_title"></span>OTS\_推送\_包括\_安装程序\_标题  
如果设置，CPSUI 包含单词"设置"按钮的名称字符串后面 (**pName** OPTITEM 中)。

<span id="OTS_PUSH_NO_DOT_DOT_DOT"></span><span id="ots_push_no_dot_dot_dot"></span>OTS\_推送\_否\_点\_点\_点  
如果设置，CPSUI 包括三个点 （...） 按钮的名称字符串后面 (**pName** OPTITEM 中)。

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
<td><p>下压按钮框</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容加上 3</p></td>
<td><p>下压按钮图标</p></td>
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

 

 




