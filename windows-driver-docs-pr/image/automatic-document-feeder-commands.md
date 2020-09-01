---
title: 自动文档送纸器命令
description: 自动文档送纸器命令
ms.assetid: dd6664d6-4853-4f97-85cc-39a7879d523e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1932b2d9739f6f2fd24dd993c6c8c282b1f5ef83
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187197"
---
# <a name="automatic-document-feeder-commands"></a>自动文档送纸器命令


## <span id="ddk_automatic_document_feeder_commands_si"></span><span id="DDK_AUTOMATIC_DOCUMENT_FEEDER_COMMANDS_SI"></span>


本部分中的命令适用于支持自动文档送纸器 (ADF) 的 microdrivers。 若要报告 microdriver 支持自动文档送纸器，请将[**SCANINFO**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)结构中的**ADF**成员设置为 1 (或者2（如果 ADF 在 CMD INITIALIZE 命令期间有双面打印) ） \_ 。 这将导致 WIA 平板驱动程序为 ADF 控制添加所需的属性，并使用本部分中的命令。

<span id="CMD_LOAD_ADF"></span><span id="cmd_load_adf"></span>CMD \_ 负载 \_ ADF  
由 WIA 平板驱动程序调用以将页面加载到 ADF。 如果此命令不适用于设备，请返回 E \_ NOTIMPL。 对于自动馈送页面的设备，此命令是可选的。

<span id="CMD_UNLOAD_ADF"></span><span id="cmd_unload_adf"></span>CMD \_ 卸载 \_ ADF  
由 WIA 平板驱动程序调用，以从 ADF 中卸载页面。 如果此命令不适用于设备，请返回 E \_ NOTIMPL。 对于自动 unfeeds 页面的设备，此命令是可选的。

<span id="CMD_GETADFAVAILABLE"></span><span id="cmd_getadfavailable"></span>CMD \_ GETADFAVAILABLE  
由 WIA 平板驱动程序调用，用于确定 ADF 是否可供使用。 如果 ADF 可用，则返回 \_ "OK"。 如果此命令不适用于设备，请返回 E \_ NOTIMPL。

<span id="CMD_GETADFHASPAPER"></span><span id="cmd_getadfhaspaper"></span>CMD \_ GETADFHASPAPER  
由 WIA 平板驱动程序调用以获取设备 ADF 的纸张状态。 将传递的[**VAL**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)结构的**lVal**成员设置为适当的状态值。  (查看 CMD \_ ADFGETSTATUS 以获取可能的状态值。 ) 

<span id="CMD_GETADFOPEN"></span><span id="cmd_getadfopen"></span>CMD \_ GETADFOPEN  
与 CMD \_ GETADFREADY 相同。 WIA 平板驱动程序当前未使用此命令。

<span id="CMD_GETADFSTATUS"></span><span id="cmd_getadfstatus"></span>CMD \_ GETADFSTATUS  
由 WIA 平板驱动程序调用以获取附加到设备的 ADF 的状态。 将传递的[**VAL**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)结构的**lVal**成员设置为适当的状态值。 可能的状态值如下所示。

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
<td><p>ADF 没有纸张。</p></td>
</tr>
<tr class="even">
<td><p>MCRO_ERROR_PAPER_JAM</p></td>
<td><p>ADF 出现卡纸。</p></td>
</tr>
<tr class="odd">
<td><p>MCRO_ERROR_PAPER_PROBLEM</p></td>
<td><p>ADF 出现纸张问题。</p></td>
</tr>
<tr class="even">
<td><p>MCRO_ERROR_USER_INTERVENTION</p></td>
<td><p>用户需要与设备交互。</p></td>
</tr>
<tr class="odd">
<td><p>MCRO_STATUS_OK</p></td>
<td><p>没有要报告的错误。</p></td>
</tr>
</tbody>
</table>

 

<span id="CMD_GETADFUNLOADREADY"></span><span id="cmd_getadfunloadready"></span>CMD \_ GETADFUNLOADREADY  
由 WIA 平板驱动程序调用，用于确定 ADF 是否已准备好卸载页面。 如果是这样，则返回 \_ "OK"。 如果此命令不适用于设备，请返回 E \_ NOTIMPL。

 

