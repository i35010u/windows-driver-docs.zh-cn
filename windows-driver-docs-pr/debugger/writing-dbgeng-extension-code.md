---
title: 编写 DbgEng 扩展代码
description: 本部分介绍如何编写 DbgEng 扩展代码
ms.assetid: b1ee686b-986e-46eb-a4bf-93e2de6d1aeb
keywords:
- DbgEng 扩展，编写
ms.date: 10/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 901d85dde4fe9af47054687949897ad28f4602e4
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916112"
---
# <a name="writing-dbgeng-extension-code"></a>编写 DbgEng 扩展代码

## <span id="ddk_writing_dbgeng_extension_code_dbx"></span><span id="DDK_WRITING_DBGENG_EXTENSION_CODE_DBX"></span>

[DbgEng 扩展](debugger-engine-and-extension-apis.md)命令可以包含任何标准C++代码。 它们还可以包括显示C++在 dbgeng 头文件中的接口，以及 wdbgexts 标头文件中显示的 C 函数。

如果要使用 wdbgexts 中的函数，则需要在包含 wdbgexts 之前定义 KDEXT\_64 位。 例如：

```cpp
#define KDEXT_64BIT
#include wdbgexts.h
#include dbgeng.h
```

有关可在扩展命令中使用的 dbgeng 中的接口的完整列表，请参阅[调试器引擎参考](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-engine-reference)。

有关 wdbgexts 中可在扩展命令中使用的函数的完整列表，请参阅[Wdbgexts 函数](https://docs.microsoft.com/windows-hardware/drivers/debugger/wdbgexts-functions)。 在32位版本和64位版本中，会显示多个函数。 通常，64位版本以 "64" 结尾，而32位版本没有数字结尾--例如， **ReadIoSpace64**和**ReadIoSpace**。 从 DbgEng 扩展调用 wdbgexts 函数时，应始终使用以 "64" 结尾的函数名称。 这是因为无论目标平台如何，[调试器引擎](introduction.md#debugger-engine)都始终在内部使用64位指针。

如果在 DbgEng 扩展中包括 wdbgexts，则应在扩展 DLL 的初始化过程中调用[**GetWindbgExtensionApis64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getwindbgextensionapis64) （请参阅[*DebugExtensionInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nc-dbgeng-pdebug_extension_initialize)）。

**请注意**   不能尝试从任何调试器扩展调用任何 Dbghelp.dll 或 imagehlp.dll 例程。 不支持调用这些例程，这可能会导致各种问题。
