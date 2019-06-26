---
title: 访问设备接口属性
description: 访问设备接口属性
ms.assetid: 8a46816b-56c5-49e9-8250-9ede037ae2b5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92fc771822fd6e7b258d1c72596a98c4f5db5d28
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383034"
---
# <a name="accessing-device-interface-properties"></a>访问设备接口属性


在 Windows Vista 和更高版本的 Windows 中，应用程序和安装程序可以访问[设备接口属性](https://docs.microsoft.com/previous-versions/ff541409(v=vs.85))通过调用以下安装程序 Api 函数：

-   [**SetupDiGetDeviceInterfacePropertyKeys**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertykeys)

    **SetupDiGetDeviceInterfacePropertyKeys**函数检索标识设备接口实例的当前设置的设备接口属性的设备接口属性键的数组。 有关如何确定哪些属性设置为设备接口的信息，请参阅[确定该属性设置为设备接口](determining-which-properties-are-set-for-a-device-interface.md)。

-   [**SetupDiGetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)

    **SetupDiGetDeviceInterfaceProperty**函数[检索设备接口属性](retrieving-a-device-interface-property-value.md)设置设备接口。

-   [**SetupDiSetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)

    **SetupDiSetDeviceInterfaceProperty**函数[设置设备接口属性](setting-a-device-interface-property-value.md)设备接口。

有关如何访问设备接口属性对 Windows Server 2003、 Windows XP 和 Windows 2000 上的信息，请参阅访问设备接口属性。

 

 





