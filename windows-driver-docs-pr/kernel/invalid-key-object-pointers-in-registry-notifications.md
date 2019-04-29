---
title: 注册表通知中的项对象指针无效
description: 注册表通知中的项对象指针无效
ms.assetid: 96709c34-63a7-4b4e-8588-c7e8b41b5dea
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3ad92e0663df7dc22756e05fea0c29d2a1c425e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369283"
---
# <a name="invalid-key-object-pointers-in-registry-notifications"></a>注册表通知中的项对象指针无效


若要避免错误和可能存在内存损坏，注册表筛选驱动程序必须不尝试使用无效的对象指针访问密钥的对象。 本主题列出了在其中的情况**对象**注册表回调通知结构的成员可能包含未定义非**NULL**值。

筛选驱动程序的第二个参数的注册表中[ *RegistryCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff560903)例程[ **REG\_通知\_类**](https://msdn.microsoft.com/library/windows/hardware/ff560950)枚举值。 此值指示哪种类型的注册表回调通知结构的第三个参数*RegistryCallback*例程指向。 通知结构包含有关注册表操作的信息。 此结构的类型而异注册表操作正在执行的。

许多通知结构类型都包含**对象**指向密钥对象的成员。 在某些情况下，**对象**成员可以包含一个值，为非**NULL**，但不指向有效的密钥对象的指针。

### <a name="key-object-value-is-undefined"></a>键对象值是未定义

如果对的调用中的第二个参数*RegistryCallback*例程筛选驱动程序的注册表**REG\_通知\_类**枚举值的**RegNtPostCreateKeyEx**或**RegNtPostOpenKeyEx**，第三个参数是指向[ **REG\_POST\_操作\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560971)结构。 **对象**无效，此结构的成员才**状态**结构中的成员将设置为 STATUS\_成功。 任何其他**状态**值，包括非零状态代码为其**NT\_成功**宏计算结果为**TRUE**，指示的值**对象**成员是未定义。

### <a name="key-object-value-is-not-in-a-valid-state"></a>键值对对象未处于有效状态

如果注册表回调中的第二个参数是下列任一**REG\_通知\_类**枚举值**对象**注册表回调通知的成员结构指向密钥对象被销毁和其引用计数为零：

-   **RegNtPreKeyHandleClose** ([**REG\_KEY\_HANDLE\_CLOSE\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff560943) structure)

-   **RegNtPostKeyHandleClose** ([**REG\_POST\_OPERATION\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff560971) structure)

-   **RegNtCallbackObjectContextCleanup** ([**REG\_CALLBACK\_CONTEXT\_CLEANUP\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff560919) structure)

因为**对象**未处于有效状态，筛选驱动程序注册表对密钥对象的成员指向必须传递**对象**作为参数的指针值[Windows 驱动程序支持例程](https://msdn.microsoft.com/library/windows/hardware/ff558686)(例如， **ObReferenceObjectByPointer**)。

但是，在[ *RegistryCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff560903)调用以处理**RegNtPreKeyHandleClose**或者**RegNtPostKeyHandleClose**通知，注册表筛选器驱动程序可以调用[配置管理器例程](https://msdn.microsoft.com/library/windows/hardware/ff542038)(例如， [ **CmGetBoundTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff541905)) 采用注册表对象作为参数。

 

 




