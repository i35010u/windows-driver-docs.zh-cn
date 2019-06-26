---
title: 注册通知
description: 注册通知
ms.assetid: 06109726-77e8-49de-9486-4fa2a5aceb1c
keywords:
- 筛选注册表调用 WDK 内核，注册通知
- 注册表筛选驱动程序 WDK 内核，注册通知
- 注册筛选器的注册表调用通知
- 预先通知选项 WDK 筛选器注册表调用
- 通知后选项 WDK 筛选器注册表调用
- 通知 WDK 筛选注册表调用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5e37e58882ae9f7c1040406609fe837c6084b58
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373463"
---
# <a name="registering-for-notifications"></a>注册通知


若要筛选注册表调用，内核模式注册表筛选驱动程序必须首先调用[ **CmRegisterCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmregistercallback)或[ **CmRegisterCallbackEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmregistercallbackex)注册[ **RegistryCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ex_callback_function)例程。 (对于 Windows Vista 及更高版本的操作系统版本，驱动程序应使用**CmRegisterCallbackEx**而不是**CmRegisterCallback**。)

您的驱动程序已注册后*RegistryCallback*例程，配置管理器调用例程每个线程尝试执行注册表操作的时间。 执行注册表操作的线程可以是从调用注册表例程的用户模式下的用户模式应用程序 (**RegCreateKeyEx**， **RegOpenKeyEx**，依次类推) 和从调用的驱动程序内核模式注册表例程 ([**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)， [ **ZwOpenKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkey)，依此类推)。

对于大多数操作，您的驱动程序可以接收通知之前的配置管理器正在处理注册表操作 (*前通知*) 或立即在操作完成后 （但在之前配置管理器返回给调用方 —*通知后*)。 您的驱动程序可以接收的通知类型的列表，请参阅[ **REG\_通知\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_reg_notify_class)。

驱动程序已调用后**CmRegisterCallback**或**CmRegisterCallbackEx**，该驱动程序将收到通知，直到它调用[ **CmUnRegisterCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmunregistercallback)或已被卸载。

 

 




