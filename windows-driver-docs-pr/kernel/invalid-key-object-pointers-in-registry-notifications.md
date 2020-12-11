---
title: 注册表通知中的项对象指针无效
description: 注册表通知中的项对象指针无效
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5918f3a3d9be8d7484747c18da5c4aa6c70024b6
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091074"
---
# <a name="invalid-key-object-pointers-in-registry-notifications"></a>注册表通知中的项对象指针无效


若要避免严重错误和可能的内存损坏，注册表筛选驱动程序不得尝试使用无效的对象指针访问密钥对象。 本主题列出了注册表回调通知结构的 **对象** 成员可能包含未定义的非 **NULL** 值的情况。

在注册表筛选驱动程序中， [*RegistryCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function) 例程的第二个参数是 [**REG \_ 通知 \_ 类**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_reg_notify_class) 枚举值。 此值指示 *RegistryCallback* 例程的第三个参数所指向的注册表回调通知的类型。 通知结构包含有关注册表操作的信息。 此结构的类型根据正在执行的注册表操作而有所不同。

许多通知结构类型都包含指向密钥对象的 **对象** 成员。 在某些情况下， **对象** 成员可以包含非 **NULL** 值，但不是指向有效密钥对象的指针。

### <a name="key-object-value-is-undefined"></a>键对象值未定义

如果对注册表筛选驱动程序的 *RegistryCallback* 例程的调用中的第二个参数是 **RegNtPostCreateKeyEx** 或 **RegNtPostOpenKeyEx** 的 **reg \_ 通知 \_ 类** 枚举值，则第三个参数是指向 [**REG \_ POST \_ 操作 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_post_operation_information)结构的指针。 仅当结构的 **状态** 成员设置为状态 "成功" 时，此结构的 **对象** 成员才有效 \_ 。 任何其他 **状态值** ，包括 **NT \_ SUCCESS** 宏的计算结果为 **TRUE** 的非零状态代码，指示 **对象** 成员的值是不确定的。

### <a name="key-object-value-is-not-in-a-valid-state"></a>键对象值未处于有效状态

如果注册表回调中的第二个参数是以下 REG notification **\_ \_ 类** 枚举值之一，则注册表回调通知结构的 **对象** 成员指向正在销毁的密钥对象，其引用计数为零：

-   **RegNtPreKeyHandleClose** ([**注册表 \_ 项 \_ 处理 \_ 关闭 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_key_handle_close_information) 结构) 

-   **RegNtPostKeyHandleClose** ([**REG \_ POST \_ 操作 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_post_operation_information) 结构) 

-   **RegNtCallbackObjectContextCleanup** ([**REG \_ 回调 \_ 上下文 \_ 清理 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_callback_context_cleanup_information) 结构) 

由于 **对象** 成员指向的密钥对象处于无效状态，因此注册表筛选驱动程序不得将 **对象** 指针值作为参数传递给 [Windows 驱动程序支持例程](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer) (例如 **ObReferenceObjectByPointer**) 。

但是，在 [*RegistryCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function) 调用来处理 **RegNtPreKeyHandleClose** 或 **RegNtPostKeyHandleClose** 通知时，注册表筛选器驱动程序可以调用配置管理器例程 (例如，将注册表对象作为参数的 [**CmGetBoundTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-cmgetboundtransaction)) 。

 

