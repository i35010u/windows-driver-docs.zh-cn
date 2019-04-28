---
title: .lines（切换源行支持）
description: .Lines 命令启用或禁用对源行信息的支持。
ms.assetid: 5d923592-7aba-42a0-893b-2c6621e4b87f
keywords:
- .lines （切换源行支持） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .lines (Toggle Source Line Support)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ffb6803028bbe2e28dca3c015ca302a8c3770f5d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336202"
---
# <a name="lines-toggle-source-line-support"></a>.lines（切换源行支持）


**.Lines**命令启用或禁用对源行信息的支持。

```dbgcmd
.lines [-e|-d|-t]
```

## <a name="span-idddkmetatogglesourcelinesupportdbgspanspan-idddkmetatogglesourcelinesupportdbgspanparameters"></a><span id="ddk_meta_toggle_source_line_support_dbg"></span><span id="DDK_META_TOGGLE_SOURCE_LINE_SUPPORT_DBG"></span>参数


<span id="_______-e______"></span><span id="_______-E______"></span> **-e**   
启用源代码行支持。

<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
禁用源行支持。

<span id="_______-t______"></span><span id="_______-T______"></span> **-t**   
将源行支持打开或关闭。 如果未指定参数 **.lines**，默认行为 **.lines**命令为此切换的源行支持。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关源调试相关的命令的详细信息，请参阅[在源模式中进行调试](debugging-in-source-mode.md)。

<a name="remarks"></a>备注
-------

在可以执行源代码级别调试之前，必须启用源行支持。 这种支持使得调试器加载源行符号。

可以使用启用源行支持 **.lines**命令或[的行命令行选项](command-line-options.md)。 如果已启用源行支持，使用 **.lines**命令将禁用此支持。

默认情况下，如果不使用 **.lines**命令，WinDbg 启用源行支持，并且控制台调试器 (KD、 CDB、 NTSD) 关闭的支持。 有关如何更改此设置的详细信息，请参阅[设置符号选项](symbol-options.md)。

 

 





