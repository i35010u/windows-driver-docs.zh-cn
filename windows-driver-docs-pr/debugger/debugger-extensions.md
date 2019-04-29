---
title: 使用调试器扩展
description: 本主题介绍了如何使用调试器扩展
ms.assetid: 55de0cbd-c6ba-40af-a932-2f9e57f1e8ec
keywords: 扩展命令，调试器扩展
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61eec47cb84facca4ed21b23f43700d50af9326d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324678"
---
# <a name="using-debugger-extensions"></a>使用调试器扩展


## <span id="ddk_debugger_extensions_dbg"></span><span id="DDK_DEBUGGER_EXTENSIONS_DBG"></span>


Visual Studio、 WinDbg、 KD 和 CDB 所有允许使用的调试器扩展命令。 这些扩展让这些三个 Microsoft 调试器的功能和灵活性很大程度。

调试器扩展命令与标准调试器命令一样使用得多。 但是，调试程序二进制文件本身的一部分内置调试器命令时，调试器扩展命令公开的不同于调试器的 Dll。

这样即可将其专门针对新调试器命令写入到具体的需求。 此外，大量的调试器扩展 Dll 都附带有调试工具本身。

本部分包括：

[加载调试器扩展 Dll](loading-debugger-extension-dlls.md)

[使用调试器扩展命令](using-debugger-extension-commands.md)

[编写新的调试器扩展](writing-new-debugger-extensions.md)

 

 





