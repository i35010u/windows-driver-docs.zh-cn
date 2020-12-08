---
title: .hh（打开 HTML 帮助文件）
description: Hh 命令打开 Windows 调试工具文档。
keywords:
- hh (打开 HTML 帮助文件) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .hh (Open HTML Help File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1fdd9d927a97fe33ba00cf58ca7db2ac263e0e54
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825841"
---
# <a name="hh-open-html-help-file"></a>.hh（打开 HTML 帮助文件）


**Hh** 命令打开 Windows 调试工具文档。

```dbgcmd
.hh [Text] 
```

## <a name="span-idddk_meta_open_html_help_file_dbgspanspan-idddk_meta_open_html_help_file_dbgspanparameters"></a><span id="ddk_meta_open_html_help_file_dbg"></span><span id="DDK_META_OPEN_HTML_HELP_FILE_DBG"></span>参数


<span id="_______Text______"></span><span id="_______text______"></span><span id="_______TEXT______"></span>*文本*   
指定要在帮助文档的索引中查找的文本。

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

 

[通过 Remote.exe执行远程调试](remote-debugging-through-remote-exe.md)时，不能使用此命令。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关帮助文档的详细信息，请参阅 [使用帮助文件](using-the-help-documentation.md)。

<a name="remarks"></a>备注
-------

**Hh** 命令打开 Windows 调试工具文档 () 。 如果指定 *文本*，则调试器将在文档中打开 " **索引** " 窗格，并在索引中搜索 *文本* 作为关键字。 如果不指定 *文本*，调试器将打开文档的 **内容** 窗格。

 

 





