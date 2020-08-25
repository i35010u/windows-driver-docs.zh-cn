---
title: TVOT \_ 按键
description: TVOT \_ 按键
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
ms.openlocfilehash: 5f98b17db94bd1154653a654df3b89b3e393577b
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802517"
---
# <a name="tvot_pushbutton"></a>TVOT \_ 按键


## <span id="ddk_tvot_pushbutton_gg"></span><span id="DDK_TVOT_PUSHBUTTON_GG"></span>


TVOT \_ 按键选项类型包括分组框中的 "推送" 按钮。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem) 构造  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
取决于 OPTPARAM 结构的 **样式** 成员，如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>按钮样式</th>
<th>Sel/pSel 用法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_CALLBACK</p></td>
<td><p>未使用。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_DLGPROC</p></td>
<td><p>CPSUI 存储对话框过程的返回值。</p></td>
</tr>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_HTCLRADJ</p></td>
<td><p>CPSUI 存储半色调运算的返回值。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_HTSETUP</p></td>
<td><p>CPSUI 存储半色调运算的返回值。</p></td>
</tr>
</tbody>
</table>

 

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam)结构数组 ([**OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)的**pOptParam**成员)   

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
依赖于 **样式** 成员，如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>按钮样式</th>
<th>pData 用法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_CALLBACK</p></td>
<td><p>指向 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-_cpsuicallback" data-raw-source="[&lt;strong&gt;_CPSUICALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-_cpsuicallback)"><strong>_CPSUICALLBACK</strong></a>类型的函数的指针。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_DLGPROC</p></td>
<td><p>DLGPROC-指向对话框过程的类型化指针 (参阅 Microsoft Windows SDK 文档) 。</p></td>
</tr>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_HTCLRADJ</p></td>
<td><p>指向 COLORADJUSTMENT 结构的指针 () Windows SDK 文档中所述。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_HTSETUP</p></td>
<td><p>指向 <a href="https://docs.microsoft.com/windows/win32/api/winddi/ns-winddi-_devhtadjdata" data-raw-source="[&lt;strong&gt;DEVHTADJDATA&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winddi/ns-winddi-_devhtadjdata)"><strong>DEVHTADJDATA</strong></a> 结构的指针。</p></td>
</tr>
</tbody>
</table>

 

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
标识要与 "推送" 按钮关联的图标。

<span id="___________lParam__________"></span><span id="___________lparam__________"></span><span id="___________LPARAM__________"></span> lParam   
依赖于样式成员，如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>按钮样式</th>
<th>lParam 用法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_CALLBACK</p></td>
<td><p>未使用。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_DLGPROC</p></td>
<td><p>对话框资源的资源标识符或 DLGTEMPLATE 结构的句柄 (参阅 Windows SDK 文档) 。 取决于 OPTPARAM 结构 <strong>标志</strong> 成员中的 DPF_USE_HDLGTEMPLATE 标志。</p></td>
</tr>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_HTCLRADJ</p></td>
<td><p>未使用。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_HTSETUP</p></td>
<td><p>未使用。</p></td>
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
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="___________Style__________"></span><span id="___________style__________"></span><span id="___________STYLE__________"></span> 方式</p></td>
<td><p>指定当用户单击 "推送" 按钮时 CPSUI 执行的操作。 可以是以下其中一个值：</p></td>
</tr>
<tr class="even">
<td><p><span id="PUSHBUTTON_TYPE_CALLBACK"></span><span id="pushbutton_type_callback"></span>PUSHBUTTON_TYPE_CALLBACK</p></td>
<td><p>CPSUI 调用应用程序的 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-_cpsuicallback" data-raw-source="[&lt;strong&gt;_CPSUICALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-_cpsuicallback)"><strong>_CPSUICALLBACK</strong></a>类型回调函数来处理按钮事件，并将 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_cpsuicbparam" data-raw-source="[&lt;strong&gt;CPSUICBPARAM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_cpsuicbparam)"><strong>CPSUICBPARAM</strong></a> 结构的 <strong>Reason</strong> 成员设置为 CPSUICB_REASON_PUSHBUTTON。  (CPSUI 将忽略回调函数的返回值。 ) </p></td>
</tr>
<tr class="odd">
<td><p><span id="PUSHBUTTON_TYPE_DLGPROC"></span><span id="pushbutton_type_dlgproc"></span>PUSHBUTTON_TYPE_DLGPROC</p></td>
<td><p>应用程序的对话框过程处理按钮事件。  (有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_dlgpage" data-raw-source="[&lt;strong&gt;DLGPAGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_dlgpage)"><strong>DLGPAGE</strong></a>的 "<strong>备注</strong>" 部分。 ) </p>
<p>当函数收到 WM_INITDIALOG 消息时，其 <em>lParam</em> 参数将指向 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_cpsuicbparam" data-raw-source="[&lt;strong&gt;CPSUICBPARAM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_cpsuicbparam)"><strong>CPSUICBPARAM</strong></a> 结构，并将 <strong>Reason</strong> 成员设置为 CPSUICB_REASON_DLGPROC。</p></td>
</tr>
<tr class="even">
<td><p><span id="PUSHBUTTON_TYPE_HTCLRADJ"></span><span id="pushbutton_type_htclradj"></span>PUSHBUTTON_TYPE_HTCLRADJ</p></td>
<td><p>CPSUI 显示半色调颜色调整对话框。</p></td>
</tr>
<tr class="odd">
<td><p><span id="PUSHBUTTON_TYPE_HTSETUP"></span><span id="pushbutton_type_htsetup"></span>PUSHBUTTON_TYPE_HTSETUP</p></td>
<td><p>CPSUI 显示 "设备半色调设置" 对话框。</p></td>
</tr>
</tbody>
</table>

 

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype) 构造  

<span id="___________Type__________"></span><span id="___________type__________"></span><span id="___________TYPE__________"></span> 类别   
TVOT \_ 按键

<span id="___________Count__________"></span><span id="___________count__________"></span><span id="___________COUNT__________"></span> 计   
1

<span id="___________Style__________"></span><span id="___________style__________"></span><span id="___________STYLE__________"></span> 方式   
可以指定以下可选的位标志。

<span id="OTS_PUSH_ENABLE_ALWAYS"></span><span id="ots_push_enable_always"></span>OTS \_ 推送 \_ ENABLE \_ ALWAYS  
如果设置此属性，则始终启用 "推送" 按钮，即使用户无法修改属性表页 (也是如此，即使 \_ \_ 未在 [**COMPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_compropsheetui) 结构) 中设置 CPSUIF UPDATE 权限也是如此。

"推送" 按钮的回调函数必须显示其对话框，但它不得允许用户修改。

注意：还必须在[**OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)结构的**Flags**成员中设置此标志。

<span id="OTS_PUSH_INCL_SETUP_TITLE"></span><span id="ots_push_incl_setup_title"></span>OTS \_ 推送（ \_ 含 \_ 安装程序 \_ 标题）  
如果设置此项，CPSUI 将在 OPTITEM) 中的按钮名称字符串后 (**pName** 包含单词 "Setup"。

<span id="OTS_PUSH_NO_DOT_DOT_DOT"></span><span id="ots_push_no_dot_dot_dot"></span>OTS \_ 推送 \_ 无 \_ 点 \_ 点 \_  
如果已设置，则 CPSUI 将在 OPTITEM) 中 (**pName** 后，在按钮的名称字符串后 ( ) 三个点。

<span id="BegCtrlID"></span><span id="begctrlid"></span><span id="BEGCTRLID"></span>**BegCtrlID**  
如果[**COMPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_compropsheetui)中的**pDlgPage**标识 CPSUI 提供的页面，或[**DLGPAGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_dlgpage)中的**DlgTemplateID**标识 CPSUI 提供的模板，则不使用**BegCtrlID** 。

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
<td><p>"推送" 按钮</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong> 内容 + 3</p></td>
<td><p>推送按钮图标</p></td>
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

 

有关其他信息，请参阅 [自定义 CPSUI 支持的窗口控件](https://docs.microsoft.com/windows-hardware/drivers/print/customizing-cpsui-supported-window-controls)。

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

 

 




