---
title: .ignore_missing_pages（隐藏缺少页面错误）
description: 内核内存转储具有缺少页时，.ignore_missing_pages 命令禁止显示错误消息。
ms.assetid: 74f4944e-6f0b-4541-b32f-a2da58df7f03
keywords:
- 禁止显示缺少的页面错误 (.ignore_missing_pages) 命令
- .ignore_missing_pages （取消显示缺少的页面错误） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .ignore_missing_pages (Suppress Missing Page Errors)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4ef9064462f24c7e48d6bf16bbdf9bbb9aad2488
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336469"
---
# <a name="ignoremissingpages-suppress-missing-page-errors"></a>.ignore\_缺少\_页 （取消显示缺少的页错误）


**.Ignore\_缺少\_页面**内核内存转储具有缺少页时，命令禁止显示错误消息。

```dbgcmd
.ignore_missing_pages 0
.ignore_missing_pages 1
.ignore_missing_pages 
```

## <a name="span-idddkmetasuppressmissingpageerrorsdbgspanspan-idddkmetasuppressmissingpageerrorsdbgspanparameters"></a><span id="ddk_meta_suppress_missing_page_errors_dbg"></span><span id="DDK_META_SUPPRESS_MISSING_PAGE_ERRORS_DBG"></span>参数


<span id="_______0______"></span> **0**   
内核内存转储调试时显示所有缺少的页面错误。 这是调试器的默认行为。

<span id="_______1"></span> **1**  
禁止显示调试内核内存转储时缺少的页面错误。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>转储文件仅限调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

详细了解如何调试这些转储文件，请参阅[内核内存转储](kernel-memory-dump.md)。

<a name="remarks"></a>备注
-------

不带参数， **.ignore\_缺少\_页面**显示此设置的当前状态。

 

 





