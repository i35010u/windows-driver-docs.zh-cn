---
title: 指定上下文信息
description: 指定上下文信息
ms.assetid: 7133529f-5a6c-4df1-8d03-1c79c0d98fa9
keywords:
- 筛选注册表调用 WDK 内核，上下文信息
- 注册表筛选驱动程序 WDK 内核，上下文信息
- 上下文信息
- 上下文信息 WDK 筛选注册表调用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 734645b3ec2ca323a79e063e03aac447febaf8f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838416"
---
# <a name="specifying-context-information"></a>指定上下文信息


配置管理器为注册表筛选驱动程序提供了多种方法，用于将上下文信息分配到注册表操作。 注册表筛选驱动程序可以：

-   向[*RegistryCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function)例程分配上下文信息。

    当驱动程序调用[**CmRegisterCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallback)或[**CmRegisterCallbackEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex)来注册注册操作的通知时，驱动程序可以指定驱动程序定义的上下文值。 每次配置管理器调用例程时，配置管理器都会将此上下文值传递到驱动程序的*RegistryCallback*例程。

    从 Windows XP 开始支持此上下文信息。

-   将上下文信息分配到注册表操作。

    驱动程序可以在每个**REG\_*XXX*** 的**CallContext**成员中存储特定于操作的上下文信息\_密钥\_驱动程序的*RegistryCallback*例程接收的信息结构。 如果你的驱动程序接收到注册操作的预先通知和后通知，则[**REG\_post\_操作\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_post_operation_information)结构包含指向合适的通知结构的指针。 当*RegistryCallback*例程接收到**REG\_POST\_操作\_信息**结构时，该结构的**CallContext**成员将与前通知的**CallContext**成员匹配构造.

    从 Windows Vista 开始提供这些结构的**CallContext**成员。

-   将上下文信息分配给注册表项对象。

    [*RegistryCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function)例程可将上下文信息分配给特定的注册表项对象。 如果*RegistryCallback*例程调用[**CmSetCallbackObjectContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmsetcallbackobjectcontext)来将上下文信息分配给某个密钥对象，则针对该对象的所有操作的后续通知和后通知将包含上下文值每个 REG\_的**ObjectContext**成员 **\_密钥\_信息** 结构。 如果驱动程序提供多个*RegistryCallback*例程，则驱动程序可以为一个注册表项对象为每个例程分配不同的上下文信息。

    如果驱动程序调用了**CmSetCallbackObjectContext**，则在关闭密钥对象的句柄之后，驱动程序的*RegistryCallback*例程将收到**RegNtCallbackObjectContextCleanup**通知。 为响应此通知，例程应释放为对象的上下文分配的所有资源。 当*RegistryCallback*例程的*Argument1*参数为**RegNtCallbackObjectContextCleanup**时， *Argument2*参数是指向[**REG\_回调\_上下文的指针\_清理\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_callback_context_cleanup_information)包含指向上下文的指针的信息结构。

    从 Windows Vista 开始提供**CmSetCallbackObjectContext**例程和**RegNtCallbackObjectContextCleanup**通知。

 

 




