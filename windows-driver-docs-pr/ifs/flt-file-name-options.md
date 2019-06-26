---
title: FLT_FILE_NAME_OPTIONS
description: FLT\_文件\_名称\_选项
ms.assetid: 6e21c11e-d2c8-4c57-8225-1fbc365cbbac
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 706ffbc8047ad68d702046e2e7bfa652b56da1b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370597"
---
# <a name="fltfilenameoptions"></a>FLT\_文件\_名称\_选项





FLT\_文件\_名称\_选项类型是一个位标志，用于指定的名称格式，查询方法和文件名称信息查询的标志掩码。

```cpp
typedef ULONG FLT_FILE_NAME_OPTIONS; 
#define FLT_VALID_FILE_NAME_FORMATS 0x000000ff
    #define FLT_FILE_NAME_NORMALIZED    0x01
    #define FLT_FILE_NAME_OPENED        0x02
    #define FLT_FILE_NAME_SHORT         0x03
#define FLT_VALID_FILE_NAME_QUERY_METHODS 0x0000ff00
    #define FLT_FILE_NAME_QUERY_DEFAULT     0x0100
    #define FLT_FILE_NAME_QUERY_CACHE_ONLY  0x0200
    #define FLT_FILE_NAME_QUERY_FILESYSTEM_ONLY 0x0300
    #define FLT_FILE_NAME_QUERY_ALWAYS_ALLOW_CACHE_LOOKUP 0x0400
#define FLT_VALID_FILE_NAME_FLAGS 0xff000000
    #define FLT_FILE_NAME_REQUEST_FROM_CURRENT_PROVIDER 0x01000000
    #define FLT_FILE_NAME_DO_NOT_CACHE                  0x02000000
```

0 到 7 位指示的文件格式，可以使用查询[ **FltGetFileNameFormat** ](https://docs.microsoft.com/previous-versions/ff543030(v=vs.85))宏。 有关这些格式的说明，请参阅[ **FLT\_文件\_名称\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_file_name_information)。 当前定义以下值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>FLT_FILE_NAME_NORMALIZED</p></td>
<td align="left"><p>规范化文件名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLT_FILE_NAME_OPENED</p></td>
<td align="left"><p>对此文件打开句柄时所使用的名称。 此名称不规范化。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FLT_FILE_NAME_SHORT</p></td>
<td align="left"><p>该文件 (8.3) 短名称。 文件的短名称不包括的卷名称、 目录路径或流名称。 此名称不规范化。</p></td>
</tr>
</tbody>
</table>

 

8 到 15 位指定要由筛选器管理器，可通过使用查询的文件名称查询方法[ **FltGetFileNameQueryMethod** ](https://docs.microsoft.com/previous-versions/ff543040(v=vs.85))宏。 有关这些值的说明，请参阅[ **FltGetFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetfilenameinformation)。 当前定义以下值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>FLT_FILE_NAME_QUERY_DEFAULT</p></td>
<td align="left"><p>如果不是当前安全地查询文件系统中的文件名称，不执行任何操作。 否则，查询筛选器管理器的名称缓存的文件名称信息。 如果在缓存中找不到名称，在文件系统中查询并缓存结果。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLT_FILE_NAME_QUERY_CACHE_ONLY</p></td>
<td align="left"><p>查询筛选器管理器的名称缓存的文件名称信息。 查询的文件系统。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FLT_FILE_NAME_QUERY_FILESYSTEM_ONLY</p></td>
<td align="left"><p>查询文件系统中的文件名称信息。 不查询筛选器管理器的名称缓存，并不缓存的文件系统查询的结果。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLT_FILE_NAME_QUERY_ALWAYS_ALLOW_CACHE_LOOKUP</p></td>
<td align="left"><p>查询筛选器管理器的名称缓存的文件名称信息。 如果未在缓存中，找到的名称和当前安全地执行此操作，查询文件系统中的文件名称信息和缓存的结果。</p></td>
</tr>
</tbody>
</table>

 

位 16 至 23 是当前未使用。

名称提供程序微筛选器使用位 24 31 到指定的文件名称标志。 当前定义以下值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>FLT_FILE_NAME_REQUEST_FROM_CURRENT_PROVIDER</p></td>
<td align="left"><p>名称提供程序微筛选器可以使用此标志指定的名称查询请求应重定向到其自身 （名称提供程序微筛选器） 而不是要满足的堆栈中较低级别的名称提供程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLT_FILE_NAME_DO_NOT_CACHE</p></td>
<td align="left"><p>此标志指示不应缓存查询中检索到的名称。 名称提供程序微筛选器使用此标志，因为它们的性能中间查询生成名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FLT_FILE_NAME_ALLOW_QUERY_ON_REPARSE</p></td>
<td align="left"><p>名称提供程序微筛选器可以使用此标志来指定，则可以安全地查询中的名称后即使返回 STATUS_REPARSE 创建路径。 它是调用方负责确保<strong>的文件对象的&gt;文件名</strong>字段未更改。 不要使用此标志与装入点或符号链接重新分析点。</p>
<p>此标志为适用于 Microsoft Windows Server 2003 SP1 及更高版本。 此标志也是在 Windows 2000 SP4 更新汇总 1 和更高版本上可用。</p></td>
</tr>
</tbody>
</table>

 

要求： fltkernel.h （包括 fltkernel.h）

## <a name="related-topics"></a>相关主题


[**FLT\_FILE\_NAME\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_file_name_information)

[**FltGetDestinationFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetdestinationfilenameinformation)

[**FltGetFileNameFormat**](https://docs.microsoft.com/previous-versions/ff543030(v=vs.85))

[**FltGetFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetfilenameinformation)

[**FltGetFileNameInformationUnsafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetfilenameinformationunsafe)

[**FltGetFileNameQueryMethod**](https://docs.microsoft.com/previous-versions/ff543040(v=vs.85))

 

 






