---
title: DbgEng 扩展 DLL 剖析
description: DbgEng 扩展 DLL 剖析
keywords:
- DbgEng 扩展，DLL 解析
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65f618df9c132025c4f3bfbb0a5bcd126159ceae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819329"
---
# <a name="anatomy-of-a-dbgeng-extension-dll"></a>DbgEng 扩展 DLL 剖析


## <span id="ddk_anatomy_of_a_dbgeng_extension_dll_dbx"></span><span id="DDK_ANATOMY_OF_A_DBGENG_EXTENSION_DLL_DBX"></span>


DbgEng 扩展 DLL 可导出多个回调函数，其中一些回调函数可能是扩展命令的实现。

这些扩展 Dll 由 [调试器引擎](introduction.md#debugger-engine) 加载，可在 Microsoft Windows 上执行用户模式或内核模式调试时提供额外的任务功能或自动化任务。

如果已执行 Windows 调试工具的完全安装，则可以在 \\ 安装目录的 sdk 示例 exts 子目录中找到一个名为 "exts" 的示例 DbgEng 扩展 \\ 。

### <a name="span-idextension_commandsspanspan-idextension_commandsspanextension-commands"></a><span id="extension_commands"></span><span id="EXTENSION_COMMANDS"></span>扩展命令

扩展 DLL 可以导出用于执行扩展命令的任意数量的函数。 每个函数都在 .def 文件中显式声明为导出，其名称必须完全由小写字母组成。

用于实现扩展命令的函数必须与原型 [**PDEBUG \_ extension \_ 调用**](/windows-hardware/drivers/ddi/dbgeng/nc-dbgeng-pdebug_extension_call)匹配。

这些函数按照标准 c + + 约定命名，只不过不允许使用大写字母。 导出的函数名称和扩展命令名称相同，只是扩展命令以感叹号开头 (！ ) 。 例如，当你将 myextension.dll 加载到调试器中，然后在调试器命令窗口中键入 **！ stack** 时，调试器将在 myextension.dll 中查找名为 **stack** 的导出函数。

如果尚未加载 myextension.dll，或者其他扩展 Dll 中可能存在具有相同名称的其他扩展命令，则可以在调试器中键入 **！ myextension** 命令窗口，以指示该 dll 中的扩展 DLL 和扩展命令。

### <a name="span-idother_exported_functionsspanspan-idother_exported_functionsspanother-exported-functions"></a><span id="other_exported_functions"></span><span id="OTHER_EXPORTED_FUNCTIONS"></span>其他导出函数

DbgEng 扩展 DLL 必须导出 [*DebugExtensionInitialize*](/windows-hardware/drivers/ddi/dbgeng/nc-dbgeng-pdebug_extension_initialize)。 加载 DLL 时，将调用此来初始化 DLL。 DLL 可能会使用它来初始化全局变量。

扩展 DLL 可能会导出 [*DebugExtensionUninitialize*](/windows-hardware/drivers/ddi/dbgeng/nc-dbgeng-pdebug_extension_uninitialize)。 如果导出了此，则将在卸载扩展 DLL 之前调用它。 在卸载之前，DLL 可能会使用它来进行清理。

扩展 DLL 可能会导出 [*DebugExtensionNotify*](/windows-hardware/drivers/ddi/dbgeng/nc-dbgeng-pdebug_extension_notify)。 如果导出此方法，则在会话开始或结束时，以及当目标开始或停止执行时，将调用此方法。 还向客户端注册的 [IDebugEventCallbacks](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks) 对象提供这些通知。

扩展 DLL 可能会导出 [*KnownStructOutput*](/windows-hardware/drivers/ddi/dbgeng/nc-dbgeng-pdebug_extension_known_struct)。 如果导出了此，则在加载 DLL 时将调用它。 此函数返回 DLL 知道如何在一行上打印的结构的列表。 稍后可以调用它来设置这些结构的实例的格式以进行打印。

### <a name="span-idengine_procedure_for_loading_a_dbgeng_extension_dllspanspan-idengine_procedure_for_loading_a_dbgeng_extension_dllspanengine-procedure-for-loading-a-dbgeng-extension-dll"></a><span id="engine_procedure_for_loading_a_dbgeng_extension_dll"></span><span id="ENGINE_PROCEDURE_FOR_LOADING_A_DBGENG_EXTENSION_DLL"></span>用于加载 DbgEng 扩展 DLL 的引擎过程

加载扩展 DLL 时，引擎将按以下顺序调用回调函数：

1.  调用 **DebugExtensionInitialize** 可初始化扩展 DLL。

2.  如果已导出，则如果引擎具有活动会话，则会调用 **DebugExtensionNotify** ，如果该会话已挂起并且可访问，则调用。

3.  如果导出，将调用 **KnownStructOutput** 来请求 DLL 知道如何在单行上打印的结构的列表。

有关如何使用调试器来加载和卸载扩展 DLL 的信息，请参阅 [加载调试器扩展 dll](loading-debugger-extension-dlls.md) ，有关执行扩展命令的信息，请参阅 [使用调试器扩展命令](using-debugger-extension-commands.md) 。

调试器引擎将在对扩展 DLL 的调用周围放置 **try/except** 块。 这可以防止引擎在扩展代码中的某些类型的 bug 中进行保护;但由于扩展调用是在与引擎相同的线程中执行的，因此它们仍可能会导致崩溃。

 

