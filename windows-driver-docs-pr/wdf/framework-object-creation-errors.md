---
title: 框架对象创建错误
description: 框架对象创建错误
ms.assetid: f5345c88-1c3a-4b32-9c93-c252713f7641
keywords:
- framework 对象 WDK KMDF，创建错误
- 错误 WDK KMDF
- 错误 WDK KMDF，框架对象创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e652cf8a8e26819952056657c13e69f9db214bba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843122"
---
# <a name="framework-object-creation-errors"></a>框架对象创建错误


当驱动程序尝试创建框架对象失败时，对象创建方法将返回指示失败类型的 NTSTATUS 值。

如果驱动程序在[**WDF\_对象\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)结构中指定了无效的信息，框架可以返回：

<a href="" id="status-wdf-object-attributes-invalid"></a>状态\_WDF\_对象\_属性\_无效  
驱动程序指定了对象上下文名称，但上下文大小为零。

驱动程序指定了上下文大小替代值，但未提供[**WDF\_对象\_context\_类型\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_context_type_info)结构。

驱动程序在 WDF 中指定了**ContextSizeOverride**值\_对象\_属性小于 WDF\_对象的**CONTEXTSIZE**成员\_上下文\_类型\_信息结构。

驱动程序在 WDF 中指定了**ExecutionLevel**值\_对象\_属性不在有效的值范围内。

驱动程序在 WDF 中指定了**SynchronizationScope**值\_对象\_属性不在有效的值范围内。

<a href="" id="status-wdf-parent-assignment-not-allowed"></a>状态\_WDF\_父\_分配\_不允许\_  
驱动程序尝试将父对象分配给对象，但框架不允许驱动程序将父对象分配到对象类型。

<a href="" id="status-wdf-parent-already-assigned"></a>已\_分配\_父\_\_项状态  
驱动程序尝试将父对象分配给对象，但父对象已分配给该对象。

<a href="" id="status-wdf-parent-is-self"></a>状态\_WDF\_父\_\_自身  
驱动程序试图使对象成为其父对象。

<a href="" id="status-wdf-synchronization-scope-invalid"></a>状态\_WDF\_同步\_范围\_无效  
驱动程序指定了[**WDF\_同步\_范围**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ne-wdfobject-_wdf_synchronization_scope)类型的值对对象类型无效。

<a href="" id="status-wdf-execution-level-invalid"></a>状态\_WDF\_执行\_级别\_无效  
驱动程序指定了[**WDF\_执行\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ne-wdfobject-_wdf_execution_level)对对象类型无效的级别类型值。

如果任何框架定义结构的**大小**成员与结构的实际大小都不匹配，则该框架可以返回状态\_信息\_长度\_不匹配。

如果框架无法为新对象分配内存，则它可能会返回状态\_\_资源不足。

单独的对象创建方法可能还会返回其他[NTSTATUS 值](https://docs.microsoft.com/windows-hardware/drivers/kernel/ntstatus-values)。 有关每个创建方法的附加返回值的详细信息，请参阅该方法的参考页。

 

 





