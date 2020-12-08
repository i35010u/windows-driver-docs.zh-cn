---
title: 编写新的调试器扩展
description: 编写新的调试器扩展
keywords:
- 扩展命令 ( 命令) ，编写扩展
- 编写扩展命令
- dbgeng 头文件，编写扩展命令
- wdbgexts 头文件，编写扩展命令
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b946b194af51aff2ab533b7a792c86198aa5df34
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802751"
---
# <a name="writing-new-debugger-extensions"></a>编写新的调试器扩展


## <span id="ddk_writing_new_debugger_extensions_dbg"></span><span id="DDK_WRITING_NEW_DEBUGGER_EXTENSIONS_DBG"></span>


您可以通过编写扩展 DLL 来创建自己的调试命令。 例如，你可能希望编写一个命令来显示复杂的数据结构，或编写一个命令，该命令将根据特定变量或内存位置的值停止并启动目标。

调试器扩展有两种不同的类型：

-   *DbgEng 扩展*。 这些原型基于 dbgeng 头文件中的原型，还基于 wdbgexts 标头文件中的原型。

-   *WdbgExts 扩展*。 它们仅基于 wdbgexts 头文件中的原型。

有关如何编写调试器扩展的信息，请参阅 [编写 DbgEng extension](writing-dbgeng-extensions.md) 和 [编写 WdbgExts 扩展](writing-wdbgexts-extensions.md)。

 

 





