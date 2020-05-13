---
title: 调试器数据模型-FileSystem 命名空间
description: FileSystem 命名空间提供用于操作文件系统的属性和方法。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: f5695b2cb62766a0f0444c419ecf644b84e82dc4
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235337"
---
# <a name="the-filesystem-namespace"></a>FileSystem 命名空间

> [!IMPORTANT]
>  此接口处于积极开发阶段，会发生更改。
>
## <a name="summary"></a>摘要
FileSystem 命名空间提供用于操作文件系统的属性和方法。 这可从 JavaScript 用于读取或写入支持调试器扩展所需的文件。

## <a name="sample"></a>示例
有关如何使用此命名空间和这些对象的简单的端到端示例，请查看 GitHub 上的示例-https://github.com/Microsoft/WinDbg-Samples/tree/master/FileSystem 

## <a name="object-methods"></a>对象方法
|名称|返回类型|签名|说明|
|--- |--- |--- |--- |
|CreateFile|[文件](dbgmodel-object-file.md)|CreateFile （path，[处置]）|在指定的路径创建一个新文件并将其打开以进行写入。 *处置*可以是 "OpenExisting"、"CreateNew" 或 "CreateAlways" 中的一个。|
|CreateTempFile|[文件](dbgmodel-object-file.md)|CreateTempFile()|在% TEMP% 文件夹中创建一个新的临时文件，然后打开该文件进行写入。|
|CreateTextReader|[文本读取器](dbgmodel-object-text-reader.md)|CreateTextReader （文件 \| 路径，[编码]）|从给定的[文件](dbgmodel-object-file.md)对象或路径创建文本读取器，该读取器将读取指定编码的文本。 编码可以是 "Ascii"、"Utf8" 或 "Utf16" 之一。 如果未指定，则默认值为 "Ascii"。|
|CreateTextWriter|[Text Writer — 文本编写器](dbgmodel-object-text-writer.md)|CreateTextWriter （文件 \| 路径，[编码]）|从给定的[文件](dbgmodel-object-file.md)对象或路径创建文本编写器，该编写器将编写指定编码的文本。 编码可以是 "Ascii"、"Utf8" 或 "Utf16" 之一。 如果未指定，则默认值为 "Ascii"。|
|DeleteFile||DeleteFile （路径）|删除指定路径处的文件。|
|FileExists|是或否|FileExists （路径）|如果文件存在于给定路径，则返回 true 或 false|
|OpenFile|[文件](dbgmodel-object-file.md)|OpenFile （路径）|在指定的路径打开文件以进行读取。|

## <a name="object-properties"></a>对象属性
|名称|说明|
|--- |--- |
|CurrentDirectory|表示调试器进程当前工作目录的[目录](dbgmodel-object-directory.md)对象。|
|TempDirectory|一个[目录](dbgmodel-object-directory.md)对象，表示调试器进程的% TEMP% 目录。 |