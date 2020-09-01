---
title: 访问设备接口属性
description: 访问设备接口属性
ms.assetid: 8a46816b-56c5-49e9-8250-9ede037ae2b5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c88593a9a12590bc4fed06006d4ed49d5efefdba
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097163"
---
# <a name="accessing-device-interface-properties"></a>访问设备接口属性


在 Windows Vista 和更高版本的 Windows 中，应用程序和安装程序可以通过调用以下 Setupapi.log 函数来访问 [设备接口属性](/previous-versions/ff541409(v=vs.85)) ：

-   [**SetupDiGetDeviceInterfacePropertyKeys**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertykeys)

    **SetupDiGetDeviceInterfacePropertyKeys**函数检索设备接口属性键的数组，这些键标识当前为设备接口实例设置的设备接口属性。 有关如何确定为设备接口设置的属性的信息，请参阅确定为 [设备接口设置的属性](determining-which-properties-are-set-for-a-device-interface.md)。

-   [**SetupDiGetDeviceInterfaceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)

    **SetupDiGetDeviceInterfaceProperty**函数检索为设备接口设置的[设备接口属性](retrieving-a-device-interface-property-value.md)。

-   [**SetupDiSetDeviceInterfaceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)

    **SetupDiSetDeviceInterfaceProperty**函数设置设备接口的[设备接口属性](setting-a-device-interface-property-value.md)。

有关如何在 Windows Server 2003、Windows XP 和 Windows 2000 上访问设备接口属性的信息，请参阅访问设备接口属性。

 

