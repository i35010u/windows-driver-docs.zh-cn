---
title: 检索设备安装程序信息
description: 检索设备安装程序信息
ms.assetid: 95e88e4a-5a31-4d82-99ea-c9a4d7766c0f
keywords:
- 音频适配器 WDK，检索安装信息
- 适配器驱动程序 WDK 音频，检索安装信息
- 端口类音频适配器 WDK，检索安装信息
- 检索设备安装信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e093b15824168685da16d3f22b9c432887a69aa1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210415"
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

有关上述 DeviceProperty*Xxx* 值的说明，请参阅 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)。

 

