---
title: DbgEng 扩展 DLL 剖析
description: DbgEng 扩展 DLL 剖析
ms.assetid: 5131115b-b9a0-479b-9391-7ab384633d92
keywords:
- DbgEng 扩展 DLL 剖析
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53c3eb1026495e3ac357dc038986db4bb2ab07fd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367976"
---
# <a name="anatomy-of-a-dbgeng-extension-dll"></a>DbgEng 扩展 DLL 剖析


## <span id="ddk_anatomy_of_a_dbgeng_extension_dll_dbx"></span><span id="DDK_ANATOMY_OF_A_DBGENG_EXTENSION_DLL_DBX"></span>


DbgEng 扩展 DLL 导出多个回调函数，其中一些可能是扩展命令的实现。

这些扩展 Dll 由加载[调试器引擎](introduction.md#debugger-engine)和可以提供额外功能或用户模式或内核模式调试在 Microsoft Windows 上执行操作时自动运行的任务。

如果您执行的 Windows 调试工具的完整安装，可以在 sdk 中找到名为"exts"的示例 DbgEng 扩展\\示例\\exts 的安装目录的子目录。

### <a name="span-idextensioncommandsspanspan-idextensioncommandsspanextension-commands"></a><span id="extension_commands"></span><span id="EXTENSION_COMMANDS"></span>扩展命令

扩展 DLL 可能会导出任何数量的用于执行扩展命令的函数。 每个函数显式声明为.def 文件中的导出，并且其名称必须完全包含小写字母。

用于实现扩展命令的函数必须符合原型[ **PDEBUG\_扩展\_调用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nc-dbgeng-pdebug_extension_call)。

这些函数被命名为根据标准C++约定，但不允许该大写字母。 导出的函数名称和扩展命令名称完全相同，只不过扩展命令开始一个带有感叹号 （！）。 例如，您将 myextension.dll 加载到调试器，然后键入 **！ 堆栈**到调试器的命令窗口中，调试器将查找名为的导出函数**堆栈**myextension.dll 中。

如果尚未加载 myextension.dll，或如果可以与其他扩展 Dll 中具有相同名称的其他扩展命令，您可以键入 **！ myextension.stack**到调试器的命令窗口，以指示扩展 DLL 和该 DLL 中的扩展命令。

### <a name="span-idotherexportedfunctionsspanspan-idotherexportedfunctionsspanother-exported-functions"></a><span id="other_exported_functions"></span><span id="OTHER_EXPORTED_FUNCTIONS"></span>其他导出的函数

DLL 必须导出一个 DbgEng 扩展[*调用 DebugExtensionInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nc-dbgeng-pdebug_extension_initialize)。 这将调用该 DLL 加载时，以初始化 DLL。 它可能使用的 dll 初始化全局变量。

扩展 DLL 可能导出[ *DebugExtensionUninitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nc-dbgeng-pdebug_extension_uninitialize)。 如果这导出的它将卸载扩展 DLL 之前调用。 它可能会使用 DLL 卸载之前清理。

扩展 DLL 可能导出[ *DebugExtensionNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nc-dbgeng-pdebug_extension_notify)。 如果这导出，则将调用时会话开始或结束，并且目标启动或停止执行时。 这些通知还提供给[IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugeventcallbacks)对象注册客户端。

扩展 DLL 可能导出[ *KnownStructOutput*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nc-dbgeng-pdebug_extension_known_struct)。 如果这导出的它将加载 DLL 时调用。 此函数返回该 DLL 知道如何在单个行上打印的结构列表。 它可以调用更高版本，若要设置格式打印这些结构的实例。

### <a name="span-idengineprocedureforloadingadbgengextensiondllspanspan-idengineprocedureforloadingadbgengextensiondllspanengine-procedure-for-loading-a-dbgeng-extension-dll"></a><span id="engine_procedure_for_loading_a_dbgeng_extension_dll"></span><span id="ENGINE_PROCEDURE_FOR_LOADING_A_DBGENG_EXTENSION_DLL"></span>引擎用于加载 DbgEng 扩展 DLL 的过程

当加载 DLL 的扩展时，按以下顺序引擎会调用回调函数：

1.  **调用 DebugExtensionInitialize**调用以便初始化扩展 DLL。

2.  如果导出， **DebugExtensionNotify**调用当引擎出于活动会话，并再次调用，如果会话已挂起并可访问。

3.  如果导出， **KnownStructOutput**称为请求 DLL 知道如何在单个行上打印的结构的列表。

请参阅[加载的调试器扩展 Dll](loading-debugger-extension-dlls.md)了解如何使用调试器来加载和卸载扩展 DLL，并请参阅[使用调试器扩展命令](using-debugger-extension-commands.md)有关执行信息扩展命令。

调试器引擎会将**试用 / 除外**块围绕对扩展 DLL 的调用。 这可在引擎防止某些类型的扩展代码中; 中的 bug但是，在作为引擎的同一线程中执行扩展调用，因为它们可能仍会导致它崩溃。

 

 





