---
title: 自动文档送纸器命令
description: 自动文档送纸器命令
ms.assetid: dd6664d6-4853-4f97-85cc-39a7879d523e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32e6e75248d58ffef961e1e2b4c27bb6170a34c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373344"
---
# <a name="automatic-document-feeder-commands"></a>自动文档送纸器命令


## <span id="ddk_automatic_document_feeder_commands_si"></span><span id="DDK_AUTOMATIC_DOCUMENT_FEEDER_COMMANDS_SI"></span>


在本部分中的命令适用于 microdrivers 支持自动文档送纸器 (ADF)。 若要报告在 microdriver 支持自动文档送纸器，设置**ADF**中的成员[ **SCANINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff547361)期间 CMD 结构 1 （或如果 ADF 具有双面打印器 2）\_初始化命令。 这将导致 WIA 平板驱动程序添加 ADF 控件的所需的属性和使用本部分中的命令。

<span id="CMD_LOAD_ADF"></span><span id="cmd_load_adf"></span>CMD\_负载\_ADF  
由 WIA 平板驱动程序将加载到 ADF 页调用。 如果此命令不适用于设备返回 E\_NOTIMPL。 此命令是可选的自动送入页面的设备。

<span id="CMD_UNLOAD_ADF"></span><span id="cmd_unload_adf"></span>CMD\_UNLOAD\_ADF  
由要卸载来自 ADF 的页面的 WIA 平板驱动程序调用。 如果此命令不适用于设备返回 E\_NOTIMPL。 此命令是可选的自动 unfeeds 页面的设备。

<span id="CMD_GETADFAVAILABLE"></span><span id="cmd_getadfavailable"></span>CMD\_GETADFAVAILABLE  
由 WIA 平板驱动程序，以确定是否可供使用 ADF 调用。 ADF 是否可用，则返回 S\_确定。 如果此命令不适用于设备返回 E\_NOTIMPL。

<span id="CMD_GETADFHASPAPER"></span><span id="cmd_getadfhaspaper"></span>CMD\_GETADFHASPAPER  
调用 WIA 平板驱动程序来获取设备的 ADF 的纸张状态。 设置**lVal**成员传递[ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)为相应的状态的值的结构。 (请参阅 CMD\_ADFGETSTATUS 有关可能的状态值。)

<span id="CMD_GETADFOPEN"></span><span id="cmd_getadfopen"></span>CMD\_GETADFOPEN  
相同 CMD\_GETADFREADY。 WIA 平板驱动程序当前未使用此命令。

<span id="CMD_GETADFSTATUS"></span><span id="cmd_getadfstatus"></span>CMD\_GETADFSTATUS  
调用 WIA 平板驱动程序来获取附加到设备的 ADF 的状态。 设置**lVal**成员传递[ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)为相应的状态的值的结构。 可能的状态值如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MCRO_ERROR_GENERAL_ERROR</p></td>
<td><p>常规错误。</p></td>
</tr>
<tr class="even">
<td><p>MCRO_ERROR_OFFLINE</p></td>
<td><p>ADF 或设备处于脱机状态。</p></td>
</tr>
<tr class="odd">
<td><p>MCRO_ERROR_PAPER_EMPTY</p></td>
<td><p>ADF 具有缺纸。</p></td>
</tr>
<tr class="even">
<td><p>MCRO_ERROR_PAPER_JAM</p></td>
<td><p>ADF 具有纸。</p></td>
</tr>
<tr class="odd">
<td><p>MCRO_ERROR_PAPER_PROBLEM</p></td>
<td><p>ADF 具有纸张的问题。</p></td>
</tr>
<tr class="even">
<td><p>MCRO_ERROR_USER_INTERVENTION</p></td>
<td><p>用户需要与设备进行交互。</p></td>
</tr>
<tr class="odd">
<td><p>MCRO_STATUS_OK</p></td>
<td><p>不没有报告任何错误。</p></td>
</tr>
</tbody>
</table>

 

<span id="CMD_GETADFUNLOADREADY"></span><span id="cmd_getadfunloadready"></span>CMD\_GETADFUNLOADREADY  
由 WIA 平板驱动程序，以确定是否准备好进行页无法卸载 ADF 调用。 如果是这样，则返回 S\_确定。 如果此命令不适用于设备返回 E\_NOTIMPL。

 

 





