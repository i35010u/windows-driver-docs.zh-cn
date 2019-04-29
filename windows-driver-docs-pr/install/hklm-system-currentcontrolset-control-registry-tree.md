---
title: HKLM\SYSTEM\CurrentControlSet\Control 注册表树
description: HKLM\SYSTEM\CurrentControlSet\Control 注册表树包含控制系统启动的信息和设备配置的某些方面。
ms.assetid: 58eacd32-425d-4224-8d37-21e2caf124cf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28e40e0717c39243aec0df5c6e4b1ae7bc0efd97
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360597"
---
# <a name="hklmsystemcurrentcontrolsetcontrol-registry-tree"></a>HKLM\\系统\\CurrentControlSet\\控制注册表树





**HKLM\\系统\\CurrentControlSet\\控制**注册表树包含用于控制系统启动和设备配置的某些方面的信息。 特别值得关注的是以下子项：

<a href="" id="class"></a>**类**  
包含有关的信息[设备安装程序类](device-setup-classes.md)系统上。 还有一个用于每个类都将使用的安装程序类 GUID 命名的子项。 每个子项包含的信息有关的安装程序类，如类安装程序 （如果有），注册类上限筛选器驱动程序，并注册类低筛选器驱动程序。

每个类子项包含名为其他子项*软件密钥*(或，*驱动程序键*) 为每个此类系统中安装的设备实例。 每个这些软件密钥的名称使用设备实例 ID，这是一个十进制的四位数字的序号值。

<a href="" id="codeviceinstallers"></a>**CoDeviceInstallers**  
包含有关已注册的特定于类共同安装程序在系统上的信息。

<a href="" id="deviceclasses"></a>**DeviceClasses**  
包含有关设备接口在系统上的信息。 没有为每个子项[设备接口类](device-interface-classes.md)和注册设备接口类的接口的每个实例的这些子项下的条目。

 

 





