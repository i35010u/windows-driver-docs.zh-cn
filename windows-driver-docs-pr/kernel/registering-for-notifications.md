---
title: 注册通知
description: 注册通知
ms.assetid: 06109726-77e8-49de-9486-4fa2a5aceb1c
keywords:
- 筛选注册表调用 WDK 内核，注册通知
- 注册表筛选驱动程序 WDK 内核，注册通知
- 注册筛选器注册表调用通知
- 预先通知选项 WDK 筛选器注册表调用
- 后通知选项 WDK 筛选器注册表调用
- 通知 WDK 筛选器注册表调用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22cd7e06bdd7032e0bf50204019effee2e8806ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827480"
---
# <a name="registering-for-notifications"></a>注册通知


若要筛选注册表调用，内核模式注册表筛选驱动程序必须先调用[**CmRegisterCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallback)或[**CmRegisterCallbackEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex)来注册[**RegistryCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function)例程。 （对于 Windows Vista 和更高版本的操作系统版本，驱动程序应使用**CmRegisterCallbackEx**而不是**CmRegisterCallback**。）

驱动程序注册*RegistryCallback*例程后，每次线程尝试执行注册表操作时，配置管理器都将调用例程。 执行注册表操作的线程可以来自调用用户模式注册表例程（**RegCreateKeyEx**、 **RegOpenKeyEx**等）的用户模式应用程序，也可以来自调用内核模式注册表例程的驱动程序（[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)、 [**ZwOpenKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey)等）。

对于大多数操作，驱动程序可以在 configuration manager 处理注册表操作（*前通知*）之前或在操作完成后立即接收通知（但在 configuration manager 返回到调用方-*通知后*。 有关驱动程序可以接收的通知类型的列表，请参阅[**REG\_通知\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_reg_notify_class)。

驱动程序调用**CmRegisterCallback**或**CmRegisterCallbackEx**后，该驱动程序将收到通知，直到它调用[**CmUnRegisterCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmunregistercallback)或卸载。

 

 




