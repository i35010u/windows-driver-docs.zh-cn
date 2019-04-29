---
title: 编写 EngExtCpp 扩展
description: 编写 EngExtCpp 扩展
ms.assetid: ac8684f9-26a3-415f-9d96-938ebda29a27
keywords:
- EngExtCpp 扩展编写
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0afc5ef5c44130258a540645b65d5033817dabf9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379884"
---
# <a name="writing-engextcpp-extensions"></a>编写 EngExtCpp 扩展


## <span id="ddk_writing_dbgeng_extension_code_dbx"></span><span id="DDK_WRITING_DBGENG_EXTENSION_CODE_DBX"></span>


EngExtCpp 扩展插件库可以包含的任何标准C++代码。 它还包括C++会显示在 engextcpp.h 和 dbgeng.h 标头文件，此外在 wdbgexts.h 标头文件中出现 C 函数的接口。 将包含从 engextcpp.h dbgeng.h 和 wdbgexts.h。

可以扩展命令中使用的 dbgeng.h 中接口的完整列表，请参阅[调试器引擎参考](https://msdn.microsoft.com/library/windows/hardware/ff540540)。

可以扩展命令中使用的 wdbgexts.h 中的函数的完整列表，请参阅[WdbgExts 函数](https://msdn.microsoft.com/library/windows/hardware/ff561258)。 这些函数的数量显示在 32 位版本和 64 位版本。 通常情况下，64 位版本结束"64"版本和 32 位版本中的有任何数字结束-例如， **ReadIoSpace64**并**ReadIoSpace**。 在调用 wdbgexts.h 函数从 DbgEng 扩展时，应始终使用"64"结尾的函数名称。 这是因为[调试器引擎](introduction.md#debugger-engine)始终使用 64 位指针在内部，而不考虑目标平台。 当包括 wdbgexts.h，engextcpp.h 选择 64 位版本的 api。 **ExtensionApis** WDbgExts API 使用的全局变量是自动初始化进入 EngExtCpp 方法并在退出时清除。

当将 EngExtCpp 扩展用于远程 DbgEng 接口时，WDbgExts 接口将不可用， **ExtensionApis**结构可以归零。 如果希望 EngExtCpp 扩展可在此类环境中正常工作，它应避免使用 WDbgExts API。

**请注意**  必须尝试从任何调试器扩展调用任何 DbgHelp 或了内部错误的例程。 调用这些例程不受支持，可能会导致各种问题。

 

 

 





