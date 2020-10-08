---
title: 可移植 PDB 符号
description: 可移植 PDB (程序数据库) 格式描述由公共语言基础结构语言的编译器生成并由调试器使用的调试信息的编码。
ms.assetid: 511af309-4e48-445c-ab04-85d558584fd4
keywords:
- 符号，概述
ms.date: 08/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: 262411bd357e0836f05f1070e873272b0adb7088
ms.sourcegitcommit: 70830486331e3ca0f550e5ddf8c42ad7ac782841
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91813713"
---
# <a name="portable-pdb-symbols"></a>可移植 PDB 符号

从 Windows 调试器的1.0.2007.01003 版本开始，支持可移植的 PDB 符号。 可移植符号可用于向使用符号的所有常用调试器命令（例如 [x (检查符号) ](x--examine-symbols-.md)、 [Dt (显示类型) ](dt--display-type-.md) 和 [Dx (显示调试器对象模型表达式) ](dx--display-visualizer-variables-.md)提供信息。 有关可移植 PDB 格式的常规信息，请参阅 GitHub 上的 [可移植 pdb](https://github.com/dotnet/core/blob/master/Documentation/diagnostics/portable_pdb.md) 。


## <a name="the-portable-pdb-program-database-format"></a>可移植 PDB (程序数据库) 格式

可移植 PDB (程序数据库) 格式介绍了由公共语言基础结构的编译器生成的调试信息的编码 (CLI) 语言，并由调试器和其他工具使用。 格式基于 ECMA-335 分区 II 元数据标准。 它在使用相同的物理表和流布局和编码时扩展其架构。

数据的物理布局在 ECMA-335-II 第24章中进行了介绍，便携式 PDB 调试元数据格式不会对基础结构进行任何更改。 有关 ECMA-335 的详细信息，请参阅 [标准 ECMA-335 公共语言基础结构](https://www.ecma-international.org/publications/standards/Ecma-335.htm)。

有关可移植 PDB 格式的完整信息，请参阅 [可移植 pdb v1.0：格式规范](https://github.com/dotnet/corefx/blob/archive/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md)。

## <a name="code-sample-to-read-portable-pdb-files"></a>用于读取可移植 PDB 文件的代码示例

有关读取可移植 PDB 文件的代码示例，请参阅 GitHub 上的[microsoft.diasymreader.native。](https://github.com/dotnet/symreader-portable)

此可移植 Pdb 读者实现了 Microsoft.diasymreader.native 接口，如 ISymUnmanagedReader 和 ISymUnmanagedBinder。 有关这些 .NET 接口的详细信息，请参阅 [诊断符号存储 (非托管 API 参考) ](/dotnet/framework/unmanaged-api/diagnostics/)。

## <a name="see-also"></a>请参阅

[符号和符号文件](symbols-and-symbol-files.md)

[公共和专用符号](public-and-private-symbols.md)