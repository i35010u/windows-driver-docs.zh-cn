---
title: 编写新的调试器扩展
description: 编写新的调试器扩展
ms.assetid: 6a0d3478-1c7a-44e0-8e48-1334de228c64
keywords:
- 编写扩展的扩展命令 （命令）
- 编写扩展命令
- dbgeng.h 标头文件中，编写扩展命令
- wdbgexts.h 标头文件中，编写扩展命令
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 274e77cd9b973be043f44cce4ca41f4670bc1e4b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374817"
---
# <a name="writing-new-debugger-extensions"></a>编写新的调试器扩展


## <span id="ddk_writing_new_debugger_extensions_dbg"></span><span id="DDK_WRITING_NEW_DEBUGGER_EXTENSIONS_DBG"></span>


可以通过编写扩展 DLL 创建你自己的调试命令。 例如，你可能想要编写命令以显示复杂数据结构或将停止和启动根据特定变量或内存位置的值的目标的命令。

有两种不同类型的调试器扩展：

-   *DbgEng 扩展*。 这些基于 dbgeng.h 标头文件中的原型，和 wdbgexts.h 标头文件中。

-   *WdbgExts 扩展*。 这些都基于单独 wdbgexts.h 标头文件中的原型。

有关如何编写调试器扩展的信息，请参阅[编写 DbgEng 扩展](writing-dbgeng-extensions.md)并[编写 WdbgExts 扩展](writing-wdbgexts-extensions.md)。

 

 





