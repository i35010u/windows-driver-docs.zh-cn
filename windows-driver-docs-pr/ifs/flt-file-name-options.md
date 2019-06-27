---
title: FLT_FILE_NAME_OPTIONS
description: FLT\_文件\_名称\_选项
ms.assetid: 6e21c11e-d2c8-4c57-8225-1fbc365cbbac
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dabc22438898e36c8cd546280874b5f460ddb4bb
ms.sourcegitcommit: 95e3fd15d9c00a341e774d58a927856d750a35e8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2019
ms.locfileid: "67410016"
---
# <a name="fltfilenameoptions"></a>FLT\_文件\_名称\_选项

FLT_FILE_NAME_OPTIONS 类型为指定的名称格式，查询方法和文件名称信息查询的标志的标志的位掩码。

```cpp
typedef ULONG FLT_FILE_NAME_OPTIONS;
#define FLT_VALID_FILE_NAME_FORMATS                       0x000000ff
    #define FLT_FILE_NAME_NORMALIZED                      0x00000001
    #define FLT_FILE_NAME_OPENED                          0x00000002
    #define FLT_FILE_NAME_SHORT                           0x00000003
#define FLT_VALID_FILE_NAME_QUERY_METHODS                 0x0000ff00
    #define FLT_FILE_NAME_QUERY_DEFAULT                   0x00000100
    #define FLT_FILE_NAME_QUERY_CACHE_ONLY                0x00000200
    #define FLT_FILE_NAME_QUERY_FILESYSTEM_ONLY           0x00000300
    #define FLT_FILE_NAME_QUERY_ALWAYS_ALLOW_CACHE_LOOKUP 0x00000400
#define FLT_VALID_FILE_NAME_FLAGS                         0xff000000
    #define FLT_FILE_NAME_REQUEST_FROM_CURRENT_PROVIDER   0x01000000
    #define FLT_FILE_NAME_DO_NOT_CACHE                    0x02000000
    #define FLT_FILE_NAME_ALLOW_QUERY_ON_REPARSE          0x04000000
```

0 到 7 位指示的文件格式，可以使用查询[ **FltGetFileNameFormat** ](https://docs.microsoft.com/previous-versions/ff543030(v=vs.85))宏。 有关这些格式的说明，请参阅[ **FLT_FILE_NAME_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_file_name_information)。 当前定义以下值。

| 值 | 含义 |
| ----- | ------- |
| FLT_FILE_NAME_NORMALIZED | 规范化文件名称。 |
| FLT_FILE_NAME_OPENED | 对此文件打开句柄时所使用的名称。 此名称不规范化。 |
| FLT_FILE_NAME_SHORT | 该文件 (8.3) 短名称。 文件的短名称不包括的卷名称、 目录路径或流名称。 此名称不规范化。 |

8 到 15 位指定要由筛选器管理器，可通过使用查询的文件名称查询方法[ **FltGetFileNameQueryMethod** ](https://docs.microsoft.com/previous-versions/ff543040(v=vs.85))宏。 有关这些值的说明，请参阅[ **FltGetFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetfilenameinformation)。 当前定义以下值。

| ReplTest1 | 含义 |
| ----- | ------- |
| FLT_FILE_NAME_QUERY_DEFAULT | 如果不是当前安全地查询文件系统中的文件名称，不执行任何操作。 否则，查询筛选器管理器的名称缓存的文件名称信息。 如果在缓存中找不到名称，在文件系统中查询并缓存结果。 |
| FLT_FILE_NAME_QUERY_CACHE_ONLY | 查询筛选器管理器的名称缓存的文件名称信息。 查询的文件系统。 |
| FLT_FILE_NAME_QUERY_FILESYSTEM_ONLY | 查询文件系统中的文件名称信息。 不查询筛选器管理器的名称缓存，并不缓存的文件系统查询的结果。 |
| FLT_FILE_NAME_QUERY_ALWAYS_ALLOW_CACHE_LOOKUP | 查询筛选器管理器的名称缓存的文件名称信息。 如果未在缓存中，找到的名称和当前安全地执行此操作，查询文件系统中的文件名称信息和缓存的结果。 |

位 16 至 23 是当前未使用。

名称提供程序微筛选器使用位 24 31 到指定的文件名称标志。 当前定义以下值。

| ReplTest1 | 含义 |
| ----- | ------- |
| FLT_FILE_NAME_REQUEST_FROM_CURRENT_PROVIDER | 名称提供程序微筛选器可以使用此标志指定的名称查询请求应重定向到其自身 （名称提供程序微筛选器） 而不是要满足的堆栈中较低级别的名称提供程序。 |
| FLT_FILE_NAME_DO_NOT_CACHE | 此标志指示不应缓存查询中检索到的名称。 名称提供程序微筛选器使用此标志，因为它们的性能中间查询生成名称。 |
| FLT_FILE_NAME_ALLOW_QUERY_ON_REPARSE | 名称提供程序微筛选器可以使用此标志来指定，则可以安全地查询中的名称后即使返回 STATUS_REPARSE 创建路径。 它是调用方负责确保**的文件对象-> FileName**字段未更改。 不要使用此标志与装入点或符号链接重新分析点。 |

## <a name="requirements"></a>要求

|   |   |
| - | - |
| **标头** | fltkernel.h （包括 fltkernel.h） |

## <a name="related-topics"></a>相关主题

[**FLT_FILE_NAME_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_file_name_information)

[**FltGetDestinationFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetdestinationfilenameinformation)

[**FltGetFileNameFormat**](https://docs.microsoft.com/previous-versions/ff543030(v=vs.85))

[**FltGetFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetfilenameinformation)

[**FltGetFileNameInformationUnsafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetfilenameinformationunsafe)

[**FltGetFileNameQueryMethod**](https://docs.microsoft.com/previous-versions/ff543040(v=vs.85))
