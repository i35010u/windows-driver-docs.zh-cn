---
title: Storport 微型端口驱动程序中的互锁的操作
description: 许多可用于 Windows 应用程序的互锁函数都适合于 Storport 微型端口驱动程序中使用。
ms.assetid: F3868AF4-545F-4B8E-8655-5AAD888C4B40
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec536bee0a57597da45cb2b1482a15e23f458ec6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544589"
---
# <a name="interlocked-operations-in-storport-miniport-drivers"></a>Storport 微型端口驱动程序中的互锁的操作


许多可用于 Windows 应用程序的互锁函数都适合于 Storport 微型端口驱动程序中使用。 其中的大多数功能作为编译器内部函数实现和适用于将更改同步到受保护的值。

以下互锁的函数是可在微型端口驱动程序中使用。

**请注意**  函数中声明*miniport.h*或 32 位 (x86) 驱动程序，请在*storport.h*。 平台软件开发工具包 (SDK) 文档中列出的函数主题适用于仅使用参考。

 

## <a name="span-idinterlockedlogicalspanspan-idinterlockedlogicalspanlogical"></a><span id="interlocked_logical"></span><span id="INTERLOCKED_LOGICAL"></span>逻辑


[**InterlockedAnd**](https://msdn.microsoft.com/library/windows/desktop/ms683516)  
[**InterlockedAnd16**](https://msdn.microsoft.com/library/windows/desktop/ms683518)  
[**InterlockedAnd64**](https://msdn.microsoft.com/library/windows/desktop/ms683527)  
[**InterlockedOr**](https://msdn.microsoft.com/library/windows/desktop/ms683626)  
[**InterlockedOr16**](https://msdn.microsoft.com/library/windows/desktop/ms683627)  
[**InterlockedOr64**](https://msdn.microsoft.com/library/windows/desktop/ms683633)  
[**InterlockedXor**](https://msdn.microsoft.com/library/windows/desktop/ms684021)  
[**InterlockedXor16**](https://msdn.microsoft.com/library/windows/desktop/ms684024)  
[**InterlockedXor64**](https://msdn.microsoft.com/library/windows/desktop/ms684104)  
## <a name="span-idinterlockedassignmentspanspan-idinterlockedassignmentspanassignment"></a><span id="interlocked_assignment"></span><span id="INTERLOCKED_ASSIGNMENT"></span>赋值


[**InterlockedExchange**](https://msdn.microsoft.com/library/windows/desktop/ms683590)  
[**InterlockedExchange64**](https://msdn.microsoft.com/library/windows/desktop/ms683593)  
[**InterlockedExchangePointer**](https://msdn.microsoft.com/library/windows/desktop/ms683609)  
## <a name="span-idinterlockedcomparisonspanspan-idinterlockedcomparisonspancomparison"></a><span id="interlocked_comparison"></span><span id="INTERLOCKED_COMPARISON"></span>比较


[**InterlockedCompareExchange**](https://msdn.microsoft.com/library/windows/desktop/ms683560)  
**InterlockedCompareExchange16**  
[**InterlockedCompareExchange64**](https://msdn.microsoft.com/library/windows/desktop/ms683562)  
[**InterlockedCompareExchangePointer**](https://msdn.microsoft.com/library/windows/desktop/ms683568)  
## <a name="span-idinterlockedarithmeticspanspan-idinterlockedarithmeticspanarithmetic"></a><span id="interlocked_arithmetic"></span><span id="INTERLOCKED_ARITHMETIC"></span>算术运算


[**InterlockedDecrement**](https://msdn.microsoft.com/library/windows/desktop/ms683580)  
[**InterlockedDecrement64**](https://msdn.microsoft.com/library/windows/desktop/ms683581)  
[**InterlockedExchangeAdd**](https://msdn.microsoft.com/library/windows/desktop/ms683597)  
[**InterlockedExchangeAdd64**](https://msdn.microsoft.com/library/windows/desktop/ms683599)  
[**InterlockedIncrement**](https://msdn.microsoft.com/library/windows/desktop/ms683614)  
[**InterlockedIncrement64**](https://msdn.microsoft.com/library/windows/desktop/ms683615)  
 

 




