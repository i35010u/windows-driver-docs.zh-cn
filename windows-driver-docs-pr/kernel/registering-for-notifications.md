---
title: 注册通知
description: 注册通知
keywords:
- 筛选注册表调用 WDK 内核，注册通知
- 注册表筛选驱动程序 WDK 内核，注册通知
- 注册筛选器注册表调用通知
- 预先通知选项 WDK 筛选器注册表调用
- 后通知选项 WDK 筛选器注册表调用
- 通知 WDK 筛选器注册表调用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0f11bd269acc557318e3bfc52fb8fc748abb1f3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793495"
---
# <a name="registering-for-notifications"></a>注册通知


若要筛选注册表调用，内核模式注册表筛选驱动程序必须先调用 [**CmRegisterCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallback) 或 [**CmRegisterCallbackEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex) 来注册 [**RegistryCallback**](/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function) 例程。  (适用于 Windows Vista 和更高版本的操作系统版本，驱动程序应使用 **CmRegisterCallbackEx** 而不是 **CmRegisterCallback**。 ) 

驱动程序注册 *RegistryCallback* 例程后，每次线程尝试执行注册表操作时，配置管理器都将调用例程。 执行注册表操作的线程可以来自调用用户模式注册表例程的用户模式应用程序 (**RegCreateKeyEx**、 **RegOpenKeyEx** 等) ，以及调用内核模式注册表例程 ([**ZwCreateKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)、 [**ZwOpenKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey)) 等的驱动程序。

对于大多数操作，驱动程序可以在 configuration manager 处理注册表操作之前接收通知， (*前通知*) 或在操作完成后立即 (但在 configuration manager 返回到调用方之前- *通知* 之后) 。 有关驱动程序可以接收的通知类型的列表，请参阅 [**REG \_ NOTIFY \_ 类**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_reg_notify_class)。

驱动程序调用 **CmRegisterCallback** 或 **CmRegisterCallbackEx** 后，该驱动程序将收到通知，直到它调用 [**CmUnRegisterCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-cmunregistercallback) 或卸载。

 

