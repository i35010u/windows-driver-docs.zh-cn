---
title: 编写 WdbgExts 扩展代码
description: 编写 WdbgExts 扩展代码
ms.assetid: bb37ea19-8355-42f3-aca5-32cc2b3be3b2
keywords:
- WdbgExts 扩展
- WdbgExts 扩展
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01e895a8a9305905ec60e3b790bc62539e05e75b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565342"
---
# <a name="writing-wdbgexts-extension-code"></a>编写 WdbgExts 扩展代码


## <span id="ddk_writing_wdbgexts_extension_code_dbwx"></span><span id="DDK_WRITING_WDBGEXTS_EXTENSION_CODE_DBWX"></span>


WdbgExts 扩展命令可以 WdbgExts.h 标头文件中调用任何标准的 C 函数，以及出现与调试器相关的函数。

WdbgExts 函数适用于在调试器扩展命令中使用。 它们可用于控制和检查的计算机或正在调试的应用程序。 WdbgExts.h 标头文件应包含所有代码都调用这些 WdbgExts 函数。

多个这些函数具有 32 位版本和 64 位版本。 通常情况下，64 位 WdbgExts 函数的名称以结尾"64"，例如**ReadIoSpace64**。 32 位版本具有任何数字结尾，例如， **ReadIoSpace**。 如果使用的 64 位指针，应使用"64"; 以结尾的函数名称如果使用的 32 位指针，则应使用"未修饰"函数名称。 你正在编写的所有扩展，建议 64 位指针。 请参阅[32 位指针和 64 位指针](32-bit-pointers-and-64-bit-pointers.md)有关详细信息。

WdbgExts 扩展不能使用 DbgEng.h 标头文件中显示的 c + + 接口。 如果你想要使用这些接口，应改为编写 DbgEng 扩展或 EngExtCpp 扩展。 DbgEng 扩展和 EngExtCpp 扩展可以使用 DbgEng.h 中的所有接口以及 WdbgExts.h 中。 有关详细信息，请参阅[编写 DbgEng 扩展](writing-dbgeng-extensions.md)并[编写 EngExtCpp 扩展](writing-engextcpp-extensions.md)。

**请注意**  必须尝试从调试器扩展调用任何 DbgHelp 或了内部错误的例程。 这不受支持，可能会导致各种问题。

 

以下主题概述了各种类别的 WdbgExts 函数：

[WdbgExts 输入和输出](wdbgexts-input-and-output.md)

[WdbgExts 内存访问](wdbgexts-memory-access.md)

[WdbgExts 线程和进程](wdbgexts-threads-and-processes.md)

[WdbgExts 符号](wdbgexts-symbols.md)

[WdbgExts 目标信息](wdbgexts-target-information.md)

有关这些函数的完整列表，请参阅[WdbgExts 函数](https://msdn.microsoft.com/library/windows/hardware/ff561258)。

 

 





