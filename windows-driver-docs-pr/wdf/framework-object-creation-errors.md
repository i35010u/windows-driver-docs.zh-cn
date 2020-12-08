---
title: 框架对象创建错误
description: 框架对象创建错误
keywords:
- framework 对象 WDK KMDF，创建错误
- 错误 WDK KMDF
- 错误 WDK KMDF，框架对象创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a31eb2068084d1c94dc29c3b0c50dd89dd56864
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815673"
---
# <a name="framework-object-creation-errors"></a>框架对象创建错误


当驱动程序尝试创建框架对象失败时，对象创建方法将返回指示失败类型的 NTSTATUS 值。

如果驱动程序在 [**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes) 结构中指定了无效的信息，框架可以返回：

<a href="" id="status-wdf-object-attributes-invalid"></a>状态 \_ WDF \_ 对象 \_ 属性 \_ 无效  
驱动程序指定了对象上下文名称，但上下文大小为零。

驱动程序指定了上下文大小替代值，但未提供 [**WDF \_ 对象 \_ 上下文 \_ 类型 \_ 信息**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_context_type_info) 结构。

驱动程序在 WDF 对象特性中指定了 **ContextSizeOverride** 值 \_ \_ ，该对象小于 **ContextSize** wdf \_ 对象 \_ 上下文 \_ 类型 \_ 信息结构的 ContextSize 成员。

驱动程序在 WDF 对象属性中指定的 **ExecutionLevel** 值 \_ 不在 \_ 有效的值范围内。

驱动程序在 WDF 对象属性中指定的 **SynchronizationScope** 值 \_ 不在 \_ 有效的值范围内。

<a href="" id="status-wdf-parent-assignment-not-allowed"></a>\_ \_ \_ \_ 不允许状态 WDF 父 \_ 分配  
驱动程序尝试将父对象分配给对象，但框架不允许驱动程序将父对象分配到对象类型。

<a href="" id="status-wdf-parent-already-assigned"></a>状态 \_ WDF \_ 父项 \_ 已 \_ 被分配  
驱动程序尝试将父对象分配给对象，但父对象已分配给该对象。

<a href="" id="status-wdf-parent-is-self"></a>状态 \_ WDF \_ 父项 \_ 为 \_ SELF  
驱动程序试图使对象成为其父对象。

<a href="" id="status-wdf-synchronization-scope-invalid"></a>状态 \_ WDF \_ 同步 \_ 范围 \_ 无效  
驱动程序指定了 [**WDF \_ 同步 \_ 作用域**](/windows-hardware/drivers/ddi/wdfobject/ne-wdfobject-_wdf_synchronization_scope)类型的值，该值对于对象类型无效。

<a href="" id="status-wdf-execution-level-invalid"></a>状态 \_ WDF \_ 执行 \_ 级别 \_ 无效  
驱动程序指定的 [**WDF \_ 执行 \_ 级别**](/windows-hardware/drivers/ddi/wdfobject/ne-wdfobject-_wdf_execution_level)类型值对对象类型无效。

如果任何框架定义结构的 **大小** 成员与结构的实际大小都不匹配，则该框架可能返回状态 \_ 信息 \_ 长度 \_ 不匹配。

如果框架无法为新对象分配内存，则它可能会返回状态 \_ 资源不足的情况 \_ 。

单独的对象创建方法可能还会返回其他 [NTSTATUS 值](../kernel/using-ntstatus-values.md)。 有关每个创建方法的附加返回值的详细信息，请参阅该方法的参考页。

