---
title: 如何从标头文件中生成跟踪消息
description: 如何从标头文件中生成跟踪消息
ms.assetid: 00b97f26-90e2-4efe-8bba-e3ffe7ba90ea
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 564b4f70862ab858ac0fd698e91d816c3340472e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329871"
---
# <a name="how-do-i-generate-trace-messages-from-a-header-file"></a>如何从标头文件生成跟踪消息？


若要从具有文件扩展名.c、.c + +、.cpp 和.cxx 以外的源文件生成跟踪消息，请添加 **-ext**参数运行\_WPP 宏调用 Windows 软件跟踪预处理器。

例如，若要从.c 和.h 文件生成的跟踪，请使用以下语句：

```
RUN_WPP=$(SOURCES) -km -ext:.c.h
```
确保.h 文件中包含 tracewpp 需要扫描`$(SOURCES)`，或在命令行上添加它们。  
例如：

```
RUN_WPP=$(SOURCES) tracedrv.h -km -ext:.c.h
```
不要*不*包括使用-扫描指定的.h 文件： 选项为配置数据文件，例如`trace.h`。

**-Ext**参数为源文件指定 WPP 可识别的文件类型。 WPP 将忽略具有不同的文件扩展名的文件。 默认情况下，WPP 识别仅.c、.c + +、.cpp 和.cxx 文件。

在 Windows Vista 之前的 Windows 版本中此参数的值是区分大小写，因为必须列出所有用例。 例如：

```
RUN_WPP=$(SOURCES) -km -ext:.c.C.h.H
```

此外，如果标头文件与另一个源文件具有相同的名称，添加 **-preserveext**参数运行\_WPP 宏。 例如：

```
RUN_WPP=$(SOURCES) -km -ext:.c.C.h.H  -preserveext:.c.h
```

**-Preserveext**参数创建的名称时保留指定的文件扩展名[跟踪消息标头](trace-message-header-file.md)(.tmh) 文件。 此参数可防止 WPP 创建具有相同名称的多个 TMH 文件。 默认情况下，WPP 使用仅.tmh 文件扩展名，如 tracedrv.tmh。 与 **-preserveext**参数，这些文件改为命名 tracedrv.c.tmh 和 tracedrv.h.tmh。

有关运行的可选参数的完整列表\_WPP，请参阅[WPP 预处理器](wpp-preprocessor.md)。

 

 





