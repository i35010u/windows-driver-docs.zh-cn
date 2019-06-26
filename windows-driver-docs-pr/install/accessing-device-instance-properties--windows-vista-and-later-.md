---
title: 访问设备实例属性
description: 访问设备实例属性
ms.assetid: b571201a-e765-45d0-993b-5855041b4697
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a03fe0ddebf2ec762a05cfd7b2fef63ba4dc745
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359239"
---
# <a name="accessing-device-instance-properties"></a>访问设备实例属性


在 Windows Vista 和更高版本的 Windows 中，应用程序和安装程序可以访问[设备实例属性](https://docs.microsoft.com/previous-versions/ff541334(v=vs.85))通过调用以下安装程序 Api 函数：

-   [**SetupDiGetDevicePropertyKeys**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertykeys)

    **SetupDiGetDevicePropertyKeys**函数检索标识当前为设备实例设置的设备属性的设备属性键的数组。 有关如何确定哪些属性设置的设备的信息，请参阅[确定该属性设置为设备实例](determining-which-properties-are-set-for-a-device-instance.md)。

-   [**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

    **SetupDiGetDeviceProperty**函数[检索为设备实例设置的设备属性](retrieving-a-device-instance-property-value.md)。

-   [**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

    **SetupDiSetDeviceProperty**函数[设置的设备实例的设备属性](setting-a-device-instance-property-value.md)。

有关如何访问设备属性对 Windows Server 2003、 Windows XP 和 Windows 2000 上的信息，请参阅[使用 SetupAPI 和设备的属性的配置管理器](using-setupapi-and-configuration-manager-to-access-device-properties.md)。

 

 





