---
title: 检索设备安装程序信息
description: 检索设备安装程序信息
ms.assetid: 95e88e4a-5a31-4d82-99ea-c9a4d7766c0f
keywords:
- 音频适配器 WDK，检索安装信息
- 适配器驱动程序 WDK 音频，检索安装信息
- 端口类音频适配器 WDK，检索安装信息
- 检索设备安装程序信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f176bd20c8313e2981041e9554bc3ae9737c823
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355268"
---
# <a name="retrieving-device-setup-information"></a>检索设备安装程序信息


## <span id="retrieving_device_setup_information"></span><span id="RETRIEVING_DEVICE_SETUP_INFORMATION"></span>


若要从注册表检索安装信息，请适配器驱动程序可以调用[ **PcGetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcgetdeviceproperty)函数，并且微型端口驱动程序可以调用端口驱动程序[ **IPort::GetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iport-getdeviceproperty)方法。

对于任一这些调用，调用方选择的安装信息来请求通过设备属性参数设置为以下设备之一类型\_注册表\_属性枚举值从标头文件 wdm.h 中：

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

有关说明 DeviceProperty*Xxx*值更高版本，请参阅[ **IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)。

 

 




