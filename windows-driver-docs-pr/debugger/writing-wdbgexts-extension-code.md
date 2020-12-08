---
title: 编写 WdbgExts 扩展代码
description: 编写 WdbgExts 扩展代码
keywords:
- WdbgExts 扩展
- 扩展，WdbgExts
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ba61c301980b00cb6ed472197549853c1c4e150
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802747"
---
# <a name="writing-wdbgexts-extension-code"></a>编写 WdbgExts 扩展代码


## <span id="ddk_writing_wdbgexts_extension_code_dbwx"></span><span id="DDK_WRITING_WDBGEXTS_EXTENSION_CODE_DBWX"></span>


WdbgExts 扩展命令可以调用任何标准 C 函数，以及在 WdbgExts 头文件中显示的与调试器相关的函数。

WdbgExts 函数仅用于调试程序扩展命令。 它们对于控制和检查正在调试的计算机或应用程序很有用。 调用这些 WdbgExts 函数的任何代码都应包含 WdbgExts 头文件。

其中的许多函数都有32位版本以及64位版本。 通常，64位 WdbgExts 函数的名称以 "64" 结尾，例如 **ReadIoSpace64**。 32位版本没有数字结尾，例如， **ReadIoSpace**。 如果使用的是64位指针，则应使用以 "64" 结尾的函数名;如果使用的是32位指针，则应使用 "未修饰的" 函数名称。 对于正在编写的任何扩展，建议使用64位指针。 有关详细信息，请参阅 [32 位指针和64位指针](32-bit-pointers-and-64-bit-pointers.md) 。

WdbgExts 扩展无法使用出现在 DbgEng 头文件中的 c + + 接口。 如果要使用这些接口，应改为写入 DbgEng 扩展或 EngExtCpp 扩展。 DbgEng 扩展插件和 EngExtCpp 扩展都可以使用 DbgEng 中的所有接口以及 WdbgExts 中的所有接口。 有关详细信息，请参阅 [编写 DbgEng extension](writing-dbgeng-extensions.md) 和 [编写 EngExtCpp 扩展](writing-engextcpp-extensions.md)。

**注意**   不得尝试从调试器扩展调用任何 Dbghelp.dll 或 Imagehlp.dll 例程。 这不受支持，可能会导致各种问题。

 

以下主题概述了各种类别的 WdbgExts 函数：

[WdbgExts 输入和输出](wdbgexts-input-and-output.md)

[WdbgExts 内存访问](wdbgexts-memory-access.md)

[WdbgExts 线程和进程](wdbgexts-threads-and-processes.md)

[WdbgExts 符号](wdbgexts-symbols.md)

[WdbgExts 目标信息](wdbgexts-target-information.md)

有关这些函数的完整列表，请参阅 [WdbgExts 函数](wdbgexts-functions.md)。

 

 





