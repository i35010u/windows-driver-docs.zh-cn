---
title: 记录器
description: 记录器
keywords:
- 记录器，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4fa19483999ef9f54e391980e450a3c6e8c2635
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819161"
---
# <a name="logger"></a>记录器


## <span id="ddk_logger_dtoolq"></span><span id="DDK_LOGGER_DTOOLQ"></span>


可以通过两种不同的车辆激活记录器工具。 一种方法是使用独立的 Logger.exe 程序。 另一种是启动 CDB 或 WinDbg，并使用 Logexts.dll 调试程序扩展。 这两种方法都将生成相同类型的日志输出。 但是，在任何基于 NT 的操作系统上使用的最佳工具为 CDB 或 WinDbg，其中包含 Logexts.dll 扩展命令。

记录器车辆也能正常工作，但使用调试器可以使调试器的全部功能连同记录器的强大功能。

本节包括：

[使用调试器和 Logexts.dll](using-the-debugger-and-logexts-dll.md)

[使用 Logger.exe](using-logger-exe.md)

[记录器的局限性和限制](logger-restrictions-and-limitations.md)

 

 





