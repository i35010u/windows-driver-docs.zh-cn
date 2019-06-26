---
title: 注册表通知中的项对象指针无效
description: 注册表通知中的项对象指针无效
ms.assetid: 96709c34-63a7-4b4e-8588-c7e8b41b5dea
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7598a0837c6666f8422e3779cbeefa2d737cdd01
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381696"
---
# <a name="invalid-key-object-pointers-in-registry-notifications"></a>注册表通知中的项对象指针无效


若要避免错误和可能存在内存损坏，注册表筛选驱动程序必须不尝试使用无效的对象指针访问密钥的对象。 本主题列出了在其中的情况**对象**注册表回调通知结构的成员可能包含未定义非**NULL**值。

筛选驱动程序的第二个参数的注册表中[ *RegistryCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ex_callback_function)例程[ **REG\_通知\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_reg_notify_class)枚举值。 此值指示哪种类型的注册表回调通知结构的第三个参数*RegistryCallback*例程指向。 通知结构包含有关注册表操作的信息。 此结构的类型而异注册表操作正在执行的。

许多通知结构类型都包含**对象**指向密钥对象的成员。 在某些情况下，**对象**成员可以包含一个值，为非**NULL**，但不指向有效的密钥对象的指针。

### <a name="key-object-value-is-undefined"></a>键对象值是未定义

如果对的调用中的第二个参数*RegistryCallback*例程筛选驱动程序的注册表**REG\_通知\_类**枚举值的**RegNtPostCreateKeyEx**或**RegNtPostOpenKeyEx**，第三个参数是指向[ **REG\_POST\_操作\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_reg_post_operation_information)结构。 **对象**无效，此结构的成员才**状态**结构中的成员将设置为 STATUS\_成功。 任何其他**状态**值，包括非零状态代码为其**NT\_成功**宏计算结果为**TRUE**，指示的值**对象**成员是未定义。

### <a name="key-object-value-is-not-in-a-valid-state"></a>键值对对象未处于有效状态

如果注册表回调中的第二个参数是下列任一**REG\_通知\_类**枚举值**对象**注册表回调通知的成员结构指向密钥对象被销毁和其引用计数为零：

-   **RegNtPreKeyHandleClose** ([**REG\_KEY\_HANDLE\_CLOSE\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_reg_key_handle_close_information) structure)

-   **RegNtPostKeyHandleClose** ([**REG\_POST\_OPERATION\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_reg_post_operation_information) structure)

-   **RegNtCallbackObjectContextCleanup** ([**REG\_CALLBACK\_CONTEXT\_CLEANUP\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_reg_callback_context_cleanup_information) structure)

因为**对象**未处于有效状态，筛选驱动程序注册表对密钥对象的成员指向必须传递**对象**作为参数的指针值[Windows 驱动程序支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbypointer)(例如， **ObReferenceObjectByPointer**)。

但是，在[ *RegistryCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ex_callback_function)调用以处理**RegNtPreKeyHandleClose**或者**RegNtPostKeyHandleClose**通知，注册表筛选器驱动程序可以调用[配置管理器例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)(例如， [ **CmGetBoundTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmgetboundtransaction)) 采用注册表对象作为参数。

 

 




