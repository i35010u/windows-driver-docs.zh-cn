---
title: .ignore_missing_pages（隐藏缺少页面错误）
description: .Ignore_missing_pages 命令将禁止内核内存转储缺少页面时出现的错误消息。
keywords:
- 取消 .ignore_missing_pages) 命令 ( 缺少的页错误
- .ignore_missing_pages (取消) Windows 调试时丢失的页错误
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .ignore_missing_pages (Suppress Missing Page Errors)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4788b3f32a53e0f08981670c874174172bcdc2e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826959"
---
# <a name="ignore_missing_pages-suppress-missing-page-errors"></a>。忽略 \_ 缺失 \_ 页 (取消丢失页错误) 


如果内核内存转储缺少页面，则 " **忽略 \_ 缺失 \_ 页面** " 命令将取消显示错误消息。

```dbgcmd
.ignore_missing_pages 0
.ignore_missing_pages 1
.ignore_missing_pages 
```

## <a name="span-idddk_meta_suppress_missing_page_errors_dbgspanspan-idddk_meta_suppress_missing_page_errors_dbgspanparameters"></a><span id="ddk_meta_suppress_missing_page_errors_dbg"></span><span id="DDK_META_SUPPRESS_MISSING_PAGE_ERRORS_DBG"></span>参数


<span id="_______0______"></span>**0**   
在调试内核内存转储时显示所有缺少的页错误。 这是调试器的默认行为。

<span id="_______1"></span> **1**  
禁止在调试内核内存转储时显示丢失的页错误。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅转储文件调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何调试这些转储文件的详细信息，请参阅 [内核内存转储](kernel-memory-dump.md)。

<a name="remarks"></a>备注
-------

如果没有参数，则 " **忽略 \_ 缺失 \_ 页** " 会显示此设置的当前状态。

 

 





