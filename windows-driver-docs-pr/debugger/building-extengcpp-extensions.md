---
title: 生成 EngExtCpp 扩展
description: 生成 EngExtCpp 扩展
ms.assetid: 63d73c4e-03b8-4bbe-9c2e-96cda3ad544c
keywords:
- EngExtCpp 扩展，生成
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e5372cfffba989313f5f0574dda046844396007
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837830"
---
# <a name="building-engextcpp-extensions"></a>生成 EngExtCpp 扩展


## <span id="ddk_building_dbgeng_extensions_dbx"></span><span id="DDK_BUILDING_DBGENG_EXTENSIONS_DBX"></span>


EngExtCpp 扩展库的构建方式与 DbgEng 扩展库的构建方式几乎相同。 有关详细信息，请参阅[生成 DbgEng 扩展](building-dbgeng-extensions.md)。

使用 EngExtCpp 实现代码（EngExtCpp），而不是与静态库链接。

由于 EngExtCpp 扩展框架是在 DbgEng 扩展框架的基础上构建的，因此 EngExtCpp 扩展 DLL 应导出与 DbgEng 扩展 DLL 相同的函数。

应导出每个扩展。 当使用[**EXT\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nf-engextcpp-ext_command)宏定义扩展函数时，此宏还会创建与该扩展插件同名的 C 函数。 此函数应从 DLL 导出。

以下函数由 engextcpp 提供，应从 EngExtCpp DLL 导出。

-   **DebugExtensionInitialize** --以便可以调用[**initialize**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))方法来初始化库。

-   **DebugExtensionUnitialize** --使[**初始化**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff558961(v=vs.85))方法可调用以取消初始化库。

-   **KnownStructOutputEx** --使引擎可以调用[*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))方法来设置已知结构的输出格式。

-   **DebugExtensionNotify** --使引擎可以调用[**OnSessionActive**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552312(v=vs.85))、 **OnSessionInactive**、 **OnSessionAccessible**和**OnSessionInaccessible**方法，以通知扩展库对调试会话的状态。

-   **帮助**--使 EngExtCpp 扩展框架可以自动提供 **！帮助**扩展。

即使不需要提供的功能，也可以导出这些函数。 此外，如果未导出这些功能，则它们提供的功能将丢失。

要使调试器引擎能够将 DLL 识别为有效的 DbgEng 扩展 DLL，必须导出**DebugExtensionInitialize** 。

 

 





