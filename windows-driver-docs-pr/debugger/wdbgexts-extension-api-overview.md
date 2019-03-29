---
title: WdbgExts 扩展 API 概述
description: WdbgExts 扩展 API 概述
ms.assetid: e54d330f-ab48-407f-a9f2-e4a521f5e27b
keywords:
- WdbgExts 扩展概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4abcdb6db8fdbbbd4222229cf74c5bfa9f9e704
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567246"
---
# <a name="wdbgexts-extension-api-overview"></a>WdbgExts 扩展 API 概述


## <span id="ddk_wdbgexts_extension_api_overview_dbwx"></span><span id="DDK_WDBGEXTS_EXTENSION_API_OVERVIEW_DBWX"></span>


每个 WdbgExts 扩展 DLL 导出一个或多个函数，用于实现*扩展命令*。 这些函数根据标准的 C 约定，名为，不同之处在于不允许使用大写字母。

函数名称和扩展命令名称完全相同，只不过扩展命令开始一个带有感叹号 ( **！** )。 例如，您将 Myextension.dll 加载到调试器，然后键入 **！ 堆栈**到调试器的命令窗口中，调试器将查找名为的导出函数**堆栈**Myextension.dll 中。

如果尚未加载 Myextension.dll，或者如果有与其他扩展 Dll 中具有相同名称的其他扩展命令，您可以键入 **！ myextension.stack**到调试器的命令窗口，以指示扩展 DLL 和该 DLL 中的扩展命令。

每个 WdbgExts 扩展 DLL 还将导出的大量*回调函数*。 加载 DLL 时并使用扩展命令时，将由调试器调用这些函数。

调试器引擎会将**试用 / 除外**块围绕对扩展 DLL 的调用。 这可防止某些类型的扩展代码中的 bug，引擎。 但是，由于扩展调用的执行引擎的同一线程中，仍然可能导致崩溃的引擎。

 

 





