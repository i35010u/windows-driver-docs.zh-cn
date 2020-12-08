---
title: .lines（切换源行支持）
description: Lines 命令启用或禁用对源行信息的支持。
keywords:
- " (在) Windows 调试时切换源代码行支持"
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .lines (Toggle Source Line Support)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d34c4c6e1220fa0a62963aae45568191c53c34cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804027"
---
# <a name="lines-toggle-source-line-support"></a>.lines（切换源行支持）


**Lines** 命令启用或禁用对源行信息的支持。

```dbgcmd
.lines [-e|-d|-t]
```

## <a name="span-idddk_meta_toggle_source_line_support_dbgspanspan-idddk_meta_toggle_source_line_support_dbgspanparameters"></a><span id="ddk_meta_toggle_source_line_support_dbg"></span><span id="DDK_META_TOGGLE_SOURCE_LINE_SUPPORT_DBG"></span>参数


<span id="_______-e______"></span><span id="_______-E______"></span>**-e**   
启用源行支持。

<span id="_______-d______"></span><span id="_______-D______"></span>**-d**   
禁用源行支持。

<span id="_______-t______"></span><span id="_______-T______"></span>**-t**   
启用或禁用源行支持。 如果没有为 **lines** 指定参数，则 **lines** 命令的默认行为是支持源行。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关源调试和相关命令的详细信息，请参阅 [源模式下的调试](debugging-in-source-mode.md)。

<a name="remarks"></a>备注
-------

必须先启用源行支持，然后才能执行源级调试。 此支持使调试器可以加载源行符号。

您可以通过使用 **lines** 命令或 [line 命令行选项](command-line-options.md)来启用源行支持。 如果已启用了源行支持，则使用 **lines** 命令将禁用此支持。

默认情况下，如果不使用 **lines** 命令，WinDbg 会启用源代码行支持，而控制台调试器 (KD，CDB，NTSD) 关闭支持。 有关如何更改此设置的详细信息，请参阅 [设置符号选项](symbol-options.md)。

 

 





