---
title: 在注册表中设置设备对象属性
description: 在注册表中设置设备对象属性
keywords:
- 设备对象 WDK 内核，注册表
- 注册表 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fb7a2a7aadfd675ba5a8adae0265501a593783d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822259"
---
# <a name="setting-device-object-properties-in-the-registry"></a>在注册表中设置设备对象属性





可以在注册表中设置设备对象的属性，如下所示：

-   对于 WDM 驱动程序，可以为设备的每个模型或整个设备安装程序类设置属性。  (有关设备安装程序类的详细信息，请参阅 [设备安装程序类](../install/overview-of-device-setup-classes.md)。 ) 

-   对于非 WDM 驱动程序，可以设置命名设备对象的设备安装程序类的属性。 驱动程序在创建具有 **IoCreateDeviceSecure** 的设备对象时指定设备安装程序类。 有关如何指定设备安装程序类的详细信息，请参阅 [**IoCreateDeviceSecure**](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)。

注册表中的任何设置都将覆盖驱动程序创建设备对象时提供的属性。

注册表设置由在设备安装过程中使用的 INF 文件指定，或者在安装后可通过调用 [设备安装功能](/previous-versions/ff541299(v=vs.85))的应用程序指定。

本节包含以下小节：

[在安装期间设置设备对象注册表属性](setting-device-object-registry-properties-during-installation.md)

[安装后设置设备对象注册表属性](setting-device-object-registry-properties-after-installation.md)

 

