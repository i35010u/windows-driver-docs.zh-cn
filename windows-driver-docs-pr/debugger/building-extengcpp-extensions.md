---
title: 生成 EngExtCpp 扩展
description: 生成 EngExtCpp 扩展
ms.assetid: 63d73c4e-03b8-4bbe-9c2e-96cda3ad544c
keywords:
- EngExtCpp 扩展构建
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84a512e56167b719808be5271fe45ca21d83308b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374049"
---
# <a name="building-engextcpp-extensions"></a>生成 EngExtCpp 扩展


## <span id="ddk_building_dbgeng_extensions_dbx"></span><span id="DDK_BUILDING_DBGENG_EXTENSIONS_DBX"></span>


EngExtCpp 扩展库构建几乎是相同的 DbgEng 扩展库。 有关详细信息，请参阅[构建 DbgEng 扩展](building-dbgeng-extensions.md)。

EngExtCpp 实现代码 (engextcpp.cpp) 使用而不是静态库链接。

因为 EngExtCpp 扩展框架基于 DbgEng 扩展框架，EngExtCpp 扩展动态链接库应为一个 DbgEng 扩展 DLL 导出相同的功能。

每个扩展应导出。 当你使用[ **EXT\_命令**](https://msdn.microsoft.com/library/windows/hardware/ff544514)宏来定义扩展函数，此宏还创建具有相同名称与扩展的 C 函数。 此函数应从 DLL 导出。

提供了以下函数 engextcpp 应从 EngExtCpp DLL 导出。

-   **调用 DebugExtensionInitialize** ，以便[**初始化**](https://msdn.microsoft.com/library/windows/hardware/ff550945)可以调用方法来初始化库。

-   **DebugExtensionUnitialize** ，以便[ **Uninitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff558961)可以调用方法来取消初始化库。

-   **KnownStructOutputEx** -这样，引擎可以调用[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)方法来格式化输出已知的结构。

-   **DebugExtensionNotify** -这样，引擎可以调用[ **OnSessionActive**](https://msdn.microsoft.com/library/windows/hardware/ff552312)， **OnSessionInactive**， **OnSessionAccessible**，并**OnSessionInaccessible**方法以通知的扩展库中的调试会话的状态更改。

-   **帮助**-以便可以自动提供 EngExtCpp 扩展框架 **！ 帮助**扩展。

可以导出这些函数，即使不需要提供的功能。 此外，如果它们不会导出，它们提供的功能将会丢失。

**调用 DebugExtensionInitialize**必须使调试器引擎以将 DLL 识别为有效的 DbgEng 扩展 DLL 导出。

 

 





