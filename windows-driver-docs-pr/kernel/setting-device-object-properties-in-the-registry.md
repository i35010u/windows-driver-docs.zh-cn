---
title: 在注册表中设置设备对象属性
description: 在注册表中设置设备对象属性
ms.assetid: a2cfe098-0d5d-42fb-bbdc-25376ce50a9b
keywords:
- 设备对象 WDK 内核注册表
- 注册表 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: de830ef6bae0a979b7447ccbc0e1710bdb7c3592
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521108"
---
# <a name="setting-device-object-properties-in-the-registry"></a>在注册表中设置设备对象属性





可以在注册表中，如下所示设置设备对象的属性：

-   有关 WDM 驱动程序，可以设置属性的设备，每个模型或整台设备安装程序类。 (有关设备安装程序类的详细信息，请参阅[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)。)

-   有关非 WDM 驱动程序，可以为指定的设备对象的设备安装程序类设置属性。 该驱动程序时创建的设备对象与指定设备安装程序类**IoCreateDeviceSecure**。 有关如何指定设备安装程序类的详细信息，请参阅[ **IoCreateDeviceSecure**](https://msdn.microsoft.com/library/windows/hardware/ff548407)。

在注册表中的任何设置覆盖该驱动程序创建的设备对象时提供的属性。

注册表设置指定在设备安装过程中使用的 INF 文件或可通过调用的应用程序指定安装后[设备安装函数](https://msdn.microsoft.com/library/windows/hardware/ff541299)。

本部分包含以下小节：

[在安装过程中设置设备对象注册表属性](setting-device-object-registry-properties-during-installation.md)

[安装后设置设备对象注册表属性](setting-device-object-registry-properties-after-installation.md)

 

 




