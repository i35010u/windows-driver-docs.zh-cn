---
title: .hh（打开 HTML 帮助文件）
description: .Hh * 命令将打开的 Windows 调试工具文档。
ms.assetid: 6c6d5b33-ad54-4325-93d7-ed63f9f012e8
keywords:
- .hh * （打开 HTML 帮助文件） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .hh (Open HTML Help File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6d418cb363e08b9358401f9139df9c41de6e75ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336541"
---
# <a name="hh-open-html-help-file"></a>.hh（打开 HTML 帮助文件）


**.Hh *** 命令将打开的 Windows 调试工具文档。

```dbgcmd
.hh [Text] 
```

## <a name="span-idddkmetaopenhtmlhelpfiledbgspanspan-idddkmetaopenhtmlhelpfiledbgspanparameters"></a><span id="ddk_meta_open_html_help_file_dbg"></span><span id="DDK_META_OPEN_HTML_HELP_FILE_DBG"></span>参数


<span id="_______Text______"></span><span id="_______text______"></span><span id="_______TEXT______"></span> *文本*   
指定要在索引的帮助文档中查找的文本。

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

 

当正在执行时，不能使用此命令[Remote.exe 通过远程调试](remote-debugging-through-remote-exe.md)。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关帮助文档的详细信息，请参阅[使用的帮助文件](using-the-help-documentation.md)。

<a name="remarks"></a>备注
-------

**.Hh** 命令将打开的 Windows 调试工具文档 (Debugger.chm)。 如果指定*文本*，调试器将打开**索引**窗格中的文档和搜索*文本*作为索引中的关键字。 如果未指定*文本*，调试器将打开**内容**文档中的窗格。

 

 





