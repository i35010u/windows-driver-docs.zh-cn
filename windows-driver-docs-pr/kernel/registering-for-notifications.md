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
ms.openlocfilehash: 7d05a12dd9048ba3a7949ba45556ca89d70117f8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338756"
---
# <a name="registering-for-notifications"></a>注册通知


若要筛选注册表调用，内核模式注册表筛选驱动程序必须首先调用[ **CmRegisterCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff541918)或[ **CmRegisterCallbackEx** ](https://msdn.microsoft.com/library/windows/hardware/ff541921)注册[ **RegistryCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff560903)例程。 (对于 Windows Vista 及更高版本的操作系统版本，驱动程序应使用**CmRegisterCallbackEx**而不是**CmRegisterCallback**。)

您的驱动程序已注册后*RegistryCallback*例程，配置管理器调用例程每个线程尝试执行注册表操作的时间。 执行注册表操作的线程可以是从调用注册表例程的用户模式下的用户模式应用程序 (**RegCreateKeyEx**， **RegOpenKeyEx**，依次类推) 和从调用的驱动程序内核模式注册表例程 ([**ZwCreateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566425)， [ **ZwOpenKey**](https://msdn.microsoft.com/library/windows/hardware/ff567014)，依此类推)。

对于大多数操作，您的驱动程序可以接收通知之前的配置管理器正在处理注册表操作 (*前通知*) 或立即在操作完成后 （但在之前配置管理器返回给调用方 —*通知后*)。 您的驱动程序可以接收的通知类型的列表，请参阅[ **REG\_通知\_类**](https://msdn.microsoft.com/library/windows/hardware/ff560950)。

驱动程序已调用后**CmRegisterCallback**或**CmRegisterCallbackEx**，该驱动程序将收到通知，直到它调用[ **CmUnRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff541928)或已被卸载。

 

 




