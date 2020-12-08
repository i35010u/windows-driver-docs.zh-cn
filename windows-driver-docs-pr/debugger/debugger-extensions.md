---
title: 使用调试器扩展
description: 本主题介绍如何使用调试器扩展
keywords: 扩展命令，调试器扩展
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79edf10665078ec8f93d629b95cb23d41dbe44ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809695"
---
# <a name="using-debugger-extensions"></a>使用调试器扩展


## <span id="ddk_debugger_extensions_dbg"></span><span id="DDK_DEBUGGER_EXTENSIONS_DBG"></span>


Visual Studio、WinDbg、KD 和 CDB 都允许使用调试器扩展命令。 这些扩展提供了这三个 Microsoft 调试器的强大功能和灵活性。

调试器扩展命令的使用非常类似于标准调试器命令。 但是，尽管内置调试器命令本身是调试器二进制文件的一部分，但调试器扩展命令是由不同于调试器的 Dll 公开的。

这使你可以编写根据你的特定需求定制的新调试器命令。 此外，调试工具本身还附带了大量调试器扩展 Dll。

本节包括：

[加载调试器扩展 Dll](loading-debugger-extension-dlls.md)

[使用调试器扩展命令](using-debugger-extension-commands.md)

[编写新的调试器扩展](writing-new-debugger-extensions.md)

 

 





