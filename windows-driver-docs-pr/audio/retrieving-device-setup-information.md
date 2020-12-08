---
title: 检索设备安装程序信息
description: 检索设备安装程序信息
keywords:
- 音频适配器 WDK，检索安装信息
- 适配器驱动程序 WDK 音频，检索安装信息
- 端口类音频适配器 WDK，检索安装信息
- 检索设备安装信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8472738f4ce3fa5093fadcaab4e05a64cd30508
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800699"
---
# <a name="retrieving-device-setup-information"></a>检索设备安装程序信息


## <span id="retrieving_device_setup_information"></span><span id="RETRIEVING_DEVICE_SETUP_INFORMATION"></span>


若要从注册表中检索安装信息，适配器驱动程序可以调用 [**PcGetDeviceProperty**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgetdeviceproperty) 函数，而微型端口驱动程序可以调用端口驱动程序的 [**IPort：： GetDeviceProperty**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-getdeviceproperty) 方法。

对于上述任一调用，调用方通过将设备属性参数设置为 \_ \_ 标头文件 Wdm .h 中的以下设备注册表属性枚举值之一，来选择要请求的安装程序信息的类型：

-   **DevicePropertyAddress**

-   **DevicePropertyBootConfiguration**

-   **DevicePropertyBootConfigurationTranslated**

-   **DevicePropertyBusNumber**

-   **DevicePropertyBusTypeGuid**

-   **DevicePropertyClassGuid**

-   **DevicePropertyClassName**

-   **DevicePropertyCompatibleIDs**

-   **DevicePropertyDetachability**

-   **DevicePropertyDeviceDescription**

-   **DevicePropertyDriverKeyName**

-   **DevicePropertyEnumeratorName**

-   **DevicePropertyFriendlyName**

-   **DevicePropertyHardwareID**

-   **DevicePropertyInstallState**

-   **DevicePropertyLegacyBusType**

-   **DevicePropertyLocationInformation**

-   **DevicePropertyManufacturer**

-   **DevicePropertyPhysicalDeviceObjectName**

-   **DevicePropertyUINumber**

有关上述 DeviceProperty *Xxx* 值的说明，请参阅 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)。

 

