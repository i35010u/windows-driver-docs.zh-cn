---
title: 编写 EngExtCpp 扩展
description: 编写 EngExtCpp 扩展
ms.assetid: ac8684f9-26a3-415f-9d96-938ebda29a27
keywords:
- EngExtCpp 扩展，编写
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e78b99c8deb3e5960f65cb2a2f66e13c3d43e47e
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534254"
---
# <a name="writing-engextcpp-extensions"></a>编写 EngExtCpp 扩展


## <span id="ddk_writing_dbgeng_extension_code_dbx"></span><span id="DDK_WRITING_DBGENG_EXTENSION_CODE_DBX"></span>


EngExtCpp 扩展库可以包含任何标准的 c + + 代码。 它还可以包括显示在 engextcpp 和 dbgeng 标头文件中的 c + + 接口以及 wdbgexts 头文件中显示的 C 函数。 Dbgeng 和 wdbgexts 都包含在 engextcpp 中。

有关可在扩展命令中使用的 dbgeng 中的接口的完整列表，请参阅[调试器引擎参考](debugger-engine-reference.md)。

有关 wdbgexts 中可在扩展命令中使用的函数的完整列表，请参阅[Wdbgexts 函数](wdbgexts-functions.md)。 在32位版本和64位版本中，会显示多个函数。 通常，64位版本以 "64" 结尾，而32位版本没有数字结尾--例如， **ReadIoSpace64**和**ReadIoSpace**。 从 DbgEng 扩展调用 wdbgexts 函数时，应始终使用以 "64" 结尾的函数名称。 这是因为无论目标平台如何，[调试器引擎](introduction.md#debugger-engine)都始终在内部使用64位指针。 当包含 wdbgexts 时，engextcpp 会选择64位版本的 API。 WDbgExts API 使用的**ExtensionApis**全局变量会自动初始化为输入 EngExtCpp 方法，并在退出时清除。

将 EngExtCpp 扩展与远程 DbgEng 接口一起使用时，WDbgExts 接口将不可用，并且**ExtensionApis**结构可以归零。 如果 EngExtCpp 扩展应在此类环境中正常工作，则应避免使用 WDbgExts API。

**注意**   不得尝试从任何调试器扩展调用任何 Dbghelp.dll 或 Imagehlp.dll 例程。 不支持调用这些例程，这可能会导致各种问题。

 

 

 





