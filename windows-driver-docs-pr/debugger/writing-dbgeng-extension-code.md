---
title: 编写 DbgEng 扩展代码
description: 本部分介绍如何编写 DbgEng 扩展代码
ms.assetid: b1ee686b-986e-46eb-a4bf-93e2de6d1aeb
keywords:
- DbgEng 扩展，编写
ms.date: 10/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2eeb68d94acf7acbf6df8fecb8ccb8a542e9425e
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534258"
---
# <a name="writing-dbgeng-extension-code"></a>编写 DbgEng 扩展代码

## <span id="ddk_writing_dbgeng_extension_code_dbx"></span><span id="DDK_WRITING_DBGENG_EXTENSION_CODE_DBX"></span>

[DbgEng 扩展](debugger-engine-and-extension-apis.md)命令可以包含任何标准的 c + + 代码。 它们还可以包括显示在 dbgeng 头文件中的 c + + 接口，以及 wdbgexts 标头文件中显示的 C 函数。

如果要使用 wdbgexts 中的函数，则需要在 \_ 包含 wdbgexts 之前定义 KDEXT 64 位。 例如：

```cpp
#define KDEXT_64BIT
#include wdbgexts.h
#include dbgeng.h
```

有关可在扩展命令中使用的 dbgeng 中的接口的完整列表，请参阅[调试器引擎参考](debugger-engine-reference.md)。

有关 wdbgexts 中可在扩展命令中使用的函数的完整列表，请参阅[Wdbgexts 函数](wdbgexts-functions.md)。 在32位版本和64位版本中，会显示多个函数。 通常，64位版本以 "64" 结尾，而32位版本没有数字结尾--例如， **ReadIoSpace64**和**ReadIoSpace**。 从 DbgEng 扩展调用 wdbgexts 函数时，应始终使用以 "64" 结尾的函数名称。 这是因为无论目标平台如何，[调试器引擎](introduction.md#debugger-engine)都始终在内部使用64位指针。

如果在 DbgEng 扩展中包括 wdbgexts，则应在扩展 DLL 的初始化过程中调用[**GetWindbgExtensionApis64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getwindbgextensionapis64) （请参阅[*DebugExtensionInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nc-dbgeng-pdebug_extension_initialize)）。

**注意**   不得尝试从任何调试器扩展调用任何 Dbghelp.dll 或 Imagehlp.dll 例程。 不支持调用这些例程，这可能会导致各种问题。
