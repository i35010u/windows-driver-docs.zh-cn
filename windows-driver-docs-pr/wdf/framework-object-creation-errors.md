---
title: 框架对象创建错误
description: 框架对象创建错误
ms.assetid: f5345c88-1c3a-4b32-9c93-c252713f7641
keywords:
- framework 对象 WDK KMDF，创建错误
- 错误 WDK KMDF
- WDK KMDF，framework 对象创建错误
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42e64de4ba719468dd713ad26e05e24866e7b100
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562956"
---
# <a name="framework-object-creation-errors"></a>框架对象创建错误


当驱动程序的创建 framework 对象的尝试失败时，对象创建方法将返回 NTSTATUS 值，该值指示失败类型。

如果该驱动程序指定了无效的信息在[ **WDF\_对象\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)结构，该框架可以返回：

<a href="" id="status-wdf-object-attributes-invalid"></a>状态\_WDF\_对象\_属性\_无效  
该驱动程序指定一个对象的上下文名称，但上下文大小为零。

该驱动程序指定的上下文大小重写值，但未提供[ **WDF\_对象\_上下文\_类型\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff552407)结构。

指定的驱动程序**ContextSizeOverride** WDF 中的值\_对象\_属性，它是不会早于**ContextSize** WDF 成员\_对象\_上下文\_类型\_信息结构。

指定的驱动程序**ExecutionLevel** WDF 中的值\_对象\_不在有效值范围内的属性。

指定的驱动程序**SynchronizationScope** WDF 中的值\_对象\_不在有效值范围内的属性。

<a href="" id="status-wdf-parent-assignment-not-allowed"></a>状态\_WDF\_父\_分配\_不\_允许  
驱动程序试图将父分配给对象，但该框架不允许驱动程序，以将父项分配给对象类型。

<a href="" id="status-wdf-parent-already-assigned"></a>状态\_WDF\_父\_ALREADY\_已分配  
驱动程序试图将父分配到一个对象，但父已分配给对象。

<a href="" id="status-wdf-parent-is-self"></a>STATUS\_WDF\_PARENT\_IS\_SELF  
该驱动程序尝试使其自己的父对象。

<a href="" id="status-wdf-synchronization-scope-invalid"></a>状态\_WDF\_同步\_作用域\_无效  
指定的驱动程序[ **WDF\_同步\_范围**](https://msdn.microsoft.com/library/windows/hardware/ff552518)-类型的对象类型无效的值。

<a href="" id="status-wdf-execution-level-invalid"></a>STATUS\_WDF\_EXECUTION\_LEVEL\_INVALID  
指定的驱动程序[ **WDF\_执行\_级别**](https://msdn.microsoft.com/library/windows/hardware/ff551310)-类型的对象类型无效的值。

如果**大小**框架定义的任何结构的成员与该结构的实际大小不匹配，则框架可返回状态\_信息\_长度\_不匹配。

如果框架无法为新对象分配内存，它可以返回状态\_不足\_资源。

单独的对象创建方法可能也会返回其他[NTSTATUS 值](https://msdn.microsoft.com/library/windows/hardware/ff557697)。 有关每个创建方法附加返回值的详细信息，请参阅该方法的参考页。

 

 





