---
title: 什么是 TMC 文件
description: 什么是 TMC 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b189f442ea3561d2db54290e156f7ff0142df698
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810679"
---
# <a name="what-is-the-tmc-file"></a>什么是 TMC 文件？

> [!NOTE]
> 除非使用 [TraceView](traceview.md)，否则请忽略对这些 TMC 文件的引用。

[跟踪消息控件 () 文件](trace-message-control-file.md)是一个文本文件，该文件包含[控件 GUID](control-guid.md)以及[PDB 符号文件](pdb-symbol-files.md)中表示的每个[跟踪提供程序](trace-provider.md)的跟踪级别。 TMC 文件的名称为跟踪提供程序的控件 GUID，后跟 TMC 文件扩展名。

[TraceView](traceview.md) 从 PDB 符号文件创建 [跟踪消息格式 ( tmf) 文件](trace-message-format-file.md) 时，会生成一个 TMC 文件。 使用 **-c** 选项时， [Tracepdb](tracepdb.md)还可以生成 TMC 文件。

大多数跟踪工具不使用 TMC 文件，但 TraceView 使用它将跟踪提供程序的控件 GUID 与提供程序支持的 [跟踪标志](trace-flags.md) 和 [跟踪级别](trace-level.md) 相关联。
