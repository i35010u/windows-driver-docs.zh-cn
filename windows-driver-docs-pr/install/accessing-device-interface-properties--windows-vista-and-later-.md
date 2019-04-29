---
title: 访问设备接口属性
description: 访问设备接口属性
ms.assetid: 8a46816b-56c5-49e9-8250-9ede037ae2b5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10c5e127a6c37984645f3edf6e24da09c94a686c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361189"
---
# <a name="accessing-device-interface-properties"></a>访问设备接口属性


在 Windows Vista 和更高版本的 Windows 中，应用程序和安装程序可以访问[设备接口属性](https://msdn.microsoft.com/library/windows/hardware/ff541409)通过调用以下安装程序 Api 函数：

-   [**SetupDiGetDeviceInterfacePropertyKeys**](https://msdn.microsoft.com/library/windows/hardware/ff551959)

    **SetupDiGetDeviceInterfacePropertyKeys**函数检索标识设备接口实例的当前设置的设备接口属性的设备接口属性键的数组。 有关如何确定哪些属性设置为设备接口的信息，请参阅[确定该属性设置为设备接口](determining-which-properties-are-set-for-a-device-interface.md)。

-   [**SetupDiGetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551122)

    **SetupDiGetDeviceInterfaceProperty**函数[检索设备接口属性](retrieving-a-device-interface-property-value.md)设置设备接口。

-   [**SetupDiSetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552158)

    **SetupDiSetDeviceInterfaceProperty**函数[设置设备接口属性](setting-a-device-interface-property-value.md)设备接口。

有关如何访问设备接口属性对 Windows Server 2003、 Windows XP 和 Windows 2000 上的信息，请参阅访问设备接口属性。

 

 





