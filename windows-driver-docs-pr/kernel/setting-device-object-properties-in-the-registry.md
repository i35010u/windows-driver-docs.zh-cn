---
title: 在注册表中设置设备对象属性
description: 在注册表中设置设备对象属性
ms.assetid: a2cfe098-0d5d-42fb-bbdc-25376ce50a9b
keywords:
- 设备对象 WDK 内核，注册表
- 注册表 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02756051369f359ff21a2696000a4457f8cc6d21
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838431"
---
# <a name="setting-device-object-properties-in-the-registry"></a>在注册表中设置设备对象属性





可以在注册表中设置设备对象的属性，如下所示：

-   对于 WDM 驱动程序，可以为设备的每个模型或整个设备安装程序类设置属性。 （有关设备安装程序类的详细信息，请参阅[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)。）

-   对于非 WDM 驱动程序，可以设置命名设备对象的设备安装程序类的属性。 驱动程序在创建具有**IoCreateDeviceSecure**的设备对象时指定设备安装程序类。 有关如何指定设备安装程序类的详细信息，请参阅[**IoCreateDeviceSecure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)。

注册表中的任何设置都将覆盖驱动程序创建设备对象时提供的属性。

注册表设置由在设备安装过程中使用的 INF 文件指定，或者在安装后可通过调用[设备安装功能](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))的应用程序指定。

本节包含以下小节：

[在安装过程中设置设备对象注册表属性](setting-device-object-registry-properties-during-installation.md)

[安装后设置设备对象注册表属性](setting-device-object-registry-properties-after-installation.md)

 

 




