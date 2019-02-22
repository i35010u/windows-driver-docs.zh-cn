---
title: 调试器数据模型-文件系统 Namespace
description: 文件系统命名空间提供的属性和方法，用于操作文件系统。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: d73b2b61c9846aaadcafe089b5d98fe7d8371812
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554655"
---
> [!IMPORTANT]
>  此接口处于活跃开发阶段，并将更改。
>
# <a name="the-filesystem-namespace"></a>文件系统 Namespace
## <a name="summary"></a>摘要
文件系统命名空间提供的属性和方法，用于操作文件系统。 这可以用于从 JavaScript 支持调试器扩展所需的文件读取或写入。

## <a name="sample"></a>示例
对于简单的端到端示例的如何使用此命名空间以及这些对象，请查看 GitHub-上的示例 https://github.com/Microsoft/WinDbg-Samples/tree/master/FileSystem 

## <a name="object-methods"></a>对象方法
|名称|返回类型|签名|描述|
|--- |--- |--- |--- |
|CreateFile|[file](dbgmodel-object-file.md)|CreateFile(path, [disposition])|在指定的路径创建一个新文件并将其打开进行写入。 *处置*可能是"OpenExisting"、"CreateNew"或"CreateAlways"之一。|
|CreateTempFile|[file](dbgmodel-object-file.md)|CreateTempFile()|在 %TEMP%文件夹中创建新的临时文件并将其打开进行写入。|
|CreateTextReader|[text reader](dbgmodel-object-text-reader.md)|CreateTextReader(file \| path, [encoding])|创建文本读取器从给定[文件](dbgmodel-object-file.md)对象或将读取指定的编码的文本的路径。 编码可能"Ascii"、"Utf8"或"Utf16"之一。 如果未指定，则"Ascii"是默认值。|
|CreateTextWriter|[文本编写器](dbgmodel-object-text-writer.md)|CreateTextWriter(file \| path, [encoding])|创建文本编写器从给定[文件](dbgmodel-object-file.md)对象或将写入指定的编码的文本的路径。 编码可能"Ascii"、"Utf8"或"Utf16"之一。 如果未指定，则"Ascii"是默认值。|
|DeleteFile||DeleteFile(path)|删除指定的路径中的文件。|
|FileExists|True 或 False|FileExists(path)|返回 true 或 false 并在给定的路径是否存在的文件|
|OpenFile|[file](dbgmodel-object-file.md)|OpenFile(path)|打开指定路径处文件以供读取。|

## <a name="object-properties"></a>对象属性
|名称|描述|
|--- |--- |
|CurrentDirectory|一个[directory](dbgmodel-object-directory.md)对象，表示调试器进程的当前工作目录。|
|TempDirectory|一个[directory](dbgmodel-object-directory.md)对象，表示调试器进程的 %TEMP%目录。 |