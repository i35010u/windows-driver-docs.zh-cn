---
title: WdbgExts 函数
description: WdbgExts 函数
ms.assetid: 1b070b0c-575d-4104-af66-e0a2c2f2c1b6
keywords:
- WdbgExts 扩展函数
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3308bcc0cbb5a3b01511b67b3b8282741037207f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524710"
---
# <a name="wdbgexts-functions"></a>WdbgExts 函数


## <span id="ddk_wdbgexts_functions_dbwx"></span><span id="DDK_WDBGEXTS_FUNCTIONS_DBWX"></span>


Wdbgexts.h 标头文件包含以下函数的原型。 这些函数将使用相同的原型的 32 位和 64 位扩展：

[**GetContext**](https://msdn.microsoft.com/library/windows/hardware/ff545736)

[**SetContext**](https://msdn.microsoft.com/library/windows/hardware/ff556644)

[**CheckControlC**](https://msdn.microsoft.com/library/windows/hardware/ff539072)

[**GetCurrentProcessAddr**](https://msdn.microsoft.com/library/windows/hardware/ff545779)

[**GetCurrentProcessHandle**](https://msdn.microsoft.com/library/windows/hardware/ff545816)

[**GetCurrentThreadAddr**](https://msdn.microsoft.com/library/windows/hardware/ff545889)

[**GetDebuggerCacheSize**](https://msdn.microsoft.com/library/windows/hardware/ff546568)

[**GetDebuggerData**](https://msdn.microsoft.com/library/windows/hardware/ff546573)

[**disasm**](https://msdn.microsoft.com/library/windows/hardware/ff541945)

[**dprintf**](https://msdn.microsoft.com/library/windows/hardware/ff542750)

[**GetExpression**](https://msdn.microsoft.com/library/windows/hardware/ff546683)

[**GetExpressionEx**](https://msdn.microsoft.com/library/windows/hardware/ff546691)

[**GetInputLine**](https://msdn.microsoft.com/library/windows/hardware/ff546905)

[**Ioctl**](https://msdn.microsoft.com/library/windows/hardware/ff551084)

[**GetKdContext**](https://msdn.microsoft.com/library/windows/hardware/ff546962)

[**ReadMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554287)

[**SearchMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554742)

[**WriteMemory**](https://msdn.microsoft.com/library/windows/hardware/ff561420)

[**ReadMsr**](https://msdn.microsoft.com/library/windows/hardware/ff554289)

[**WriteMsr**](https://msdn.microsoft.com/library/windows/hardware/ff561424)

[**GetPebAddress**](https://msdn.microsoft.com/library/windows/hardware/ff548122)

[**ReadPhysical**](https://msdn.microsoft.com/library/windows/hardware/ff554310)

[**ReadPhysicalWithFlags**](https://msdn.microsoft.com/library/windows/hardware/ff554315)

[**WritePhysical**](https://msdn.microsoft.com/library/windows/hardware/ff561432)

[**WritePhysicalWithFlags**](https://msdn.microsoft.com/library/windows/hardware/ff561448)

[**GetTebAddress**](https://msdn.microsoft.com/library/windows/hardware/ff549267)

[**StackTrace**](https://msdn.microsoft.com/library/windows/hardware/ff558794)

[**GetSymbol**](https://msdn.microsoft.com/library/windows/hardware/ff548447)

[**ReloadSymbols**](https://msdn.microsoft.com/library/windows/hardware/ff554381)

[**GetSetSympath**](https://msdn.microsoft.com/library/windows/hardware/ff548291)

[**TranslateVirtualToPhysical**](https://msdn.microsoft.com/library/windows/hardware/ff558914)

Wdbgexts.h 标头文件包含以下函数的原型。 这些函数具有不同的原型，32 位和 64 位扩展：

[**ReadControlSpace**](https://msdn.microsoft.com/library/windows/hardware/ff553527)

[**ReadControlSpace64**](https://msdn.microsoft.com/library/windows/hardware/ff553532)

[**ReadTypedControlSpace32**](https://msdn.microsoft.com/library/windows/hardware/ff554339)

[**ReadTypedControlSpace64**](https://msdn.microsoft.com/library/windows/hardware/ff554341)

[**WriteControlSpace**](https://msdn.microsoft.com/library/windows/hardware/ff561375)

[**ReadIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff553574)

[**ReadIoSpace64**](https://msdn.microsoft.com/library/windows/hardware/ff553577)

[**ReadIoSpaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff553580)

[**ReadIoSpaceEx64**](https://msdn.microsoft.com/library/windows/hardware/ff553583)

[**WriteIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff561406)

[**WriteIoSpace64**](https://msdn.microsoft.com/library/windows/hardware/ff561408)

[**WriteIoSpaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff561413)

[**WriteIoSpaceEx64**](https://msdn.microsoft.com/library/windows/hardware/ff561414)

[**SetThreadForOperation**](https://msdn.microsoft.com/library/windows/hardware/ff556830)

[**SetThreadForOperation64**](https://msdn.microsoft.com/library/windows/hardware/ff556832)

Wdbgexts.h 标头文件包含以下函数的原型。 仅在 64 位扩展中，可以使用这些函数：

[**GetFieldData**](https://msdn.microsoft.com/library/windows/hardware/ff546743)

[**GetFieldOffset**](https://msdn.microsoft.com/library/windows/hardware/ff546758)

[**GetFieldValue**](https://msdn.microsoft.com/library/windows/hardware/ff546781)

[**GetShortField**](https://msdn.microsoft.com/library/windows/hardware/ff548299)

[**ReadField**](https://msdn.microsoft.com/library/windows/hardware/ff553539)

[**ReadListEntry**](https://msdn.microsoft.com/library/windows/hardware/ff553585)

[**ReadPointer**](https://msdn.microsoft.com/library/windows/hardware/ff554318)

[**WritePointer**](https://msdn.microsoft.com/library/windows/hardware/ff561450)

[**IsPtr64**](https://msdn.microsoft.com/library/windows/hardware/ff551094)

[**ReadPtr**](https://msdn.microsoft.com/library/windows/hardware/ff554330)

[**GetTypeSize**](https://msdn.microsoft.com/library/windows/hardware/ff549446)

[**InitTypeRead**](https://msdn.microsoft.com/library/windows/hardware/ff550953)

[**InitTypeReadPhysical**](https://msdn.microsoft.com/library/windows/hardware/ff550957)

[**ListType**](https://msdn.microsoft.com/library/windows/hardware/ff551988)

 

 





