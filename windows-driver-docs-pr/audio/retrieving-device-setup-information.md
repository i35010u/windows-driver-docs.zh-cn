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
ms.openlocfilehash: f00508bdca84a825bfa43dee1d956d5f06edcdf1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830182"
---
# <a name="retrieving-device-setup-information"></a>检索设备安装程序信息


## <span id="retrieving_device_setup_information"></span><span id="RETRIEVING_DEVICE_SETUP_INFORMATION"></span>


若要从注册表中检索安装信息，适配器驱动程序可以调用[**PcGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgetdeviceproperty)函数，而微型端口驱动程序可以调用端口驱动程序的[**IPort：： GetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-getdeviceproperty)方法。

对于上述任一调用，调用方通过将设备属性参数设置为以下设备之一来请求要请求的安装程序信息的类型：将设备属性参数设置为以下某个设备\_注册表\_从头文件 Wdm 的属性枚举值：

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

有关上述 DeviceProperty*Xxx*值的说明，请参阅[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)。

 

 




