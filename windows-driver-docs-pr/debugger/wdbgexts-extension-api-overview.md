---
title: WdbgExts 扩展 API 概述
description: WdbgExts 扩展 API 概述
keywords:
- WdbgExts 扩展，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f4b94b420fef0c020af88c0397a045084148c1b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802849"
---
# <a name="wdbgexts-extension-api-overview"></a>WdbgExts 扩展 API 概述


## <span id="ddk_wdbgexts_extension_api_overview_dbwx"></span><span id="DDK_WDBGEXTS_EXTENSION_API_OVERVIEW_DBWX"></span>


每个 WdbgExts 扩展 DLL 都导出一个或多个用于实现 *扩展命令* 的函数。 这些函数根据标准 C 约定进行命名，只不过不允许使用大写字母。

函数名称和扩展命令名称相同，不同之处在于 extension 命令以感叹号开头 ( **！** ). 例如，当你将 Myextension.dll 加载到调试器中，然后在调试器命令窗口中键入 **！ stack** 时，调试器将在 Myextension.dll 中查找名为 **stack** 的导出函数。

如果尚未加载 Myextension.dll，或者其他扩展 Dll 中有同名的其他扩展命令，则可以在调试器中键入 **！ myextension** 命令窗口，以指示扩展 dll 和该 dll 中的扩展命令。

每个 WdbgExts 扩展 DLL 还会导出多个 *回调函数*。 这些函数是在加载 DLL 时和使用扩展命令时由调试器调用的。

调试器引擎将在对扩展 DLL 的调用周围放置 **try/except** 块。 这可以防止引擎在扩展代码中的某些类型的 bug 中。 但是，因为在与引擎相同的线程中执行扩展调用，它们仍可能会导致引擎崩溃。

 

 





