---
title: 什么是 TMC 文件
description: 什么是 TMC 文件
ms.assetid: 5927d6be-93af-4ab2-bdc1-387fabc9c5ca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dc08066c02bae9e03673e22cb02916cbf7d2065
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379135"
---
# <a name="what-is-the-tmc-file"></a>什么是 TMC 文件？

> [!NOTE]
> 除非您使用的[TraceView](traceview.md)，忽略对这些 TMC 文件的引用。

[跟踪消息控件 (.tmc) 文件](trace-message-control-file.md)是包含一个文本文件[控制 GUID](control-guid.md)以及跟踪级别的每个[跟踪提供程序](trace-provider.md)中表示[PDB 符号文件](pdb-symbol-files.md)。 TMC 文件的名称是控件的跟踪提供程序后, 跟.tmc 文件扩展名的 GUID。

[TraceView](traceview.md)创建时将生成一个 TMC 文件[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)PDB 符号文件中。 [Tracepdb](tracepdb.md)使用时，还可以生成 TMC 文件 **-c**选项。

大多数跟踪工具不使用 TMC 文件，但 TraceView 使用它将关联控件的跟踪提供程序的 GUID 与[跟踪标志](trace-flags.md)并[跟踪级别](trace-level.md)提供程序支持。
