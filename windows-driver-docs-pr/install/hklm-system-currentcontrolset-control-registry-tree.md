---
title: HKLM\SYSTEM\CurrentControlSet\Control 注册表树
description: HKLM\SYSTEM\CurrentControlSet\Control 注册表树包含用于控制系统启动和设备配置的某些方面的信息。
ms.assetid: 58eacd32-425d-4224-8d37-21e2caf124cf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff80b48420cf93804e9d7d1d3c345c4badbb2eb5
ms.sourcegitcommit: e480dcfea893ef6c85b2dfb5827f51b740466262
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71278373"
---
# <a name="hklmsystemcurrentcontrolsetcontrol-registry-tree"></a>HKLM\\系统\\CurrentControlSet\\控制注册表树





**HKLM\\system\\CurrentControlSetControl注册表树包含用于控制系统启动和设备配置的某些方面的信息。\\** 以下子项特别感兴趣：

<a href="" id="class"></a>**班级**  
包含有关系统上的[设备安装程序类](device-setup-classes.md)的信息。 使用安装程序类的 GUID 命名的每个类都有一个子项。 每个子项都包含有关安装程序类的信息，如类安装程序（如果有）、已注册的顶级筛选器驱动程序以及已注册的类低筛选器驱动程序。

<a href="" id="codeviceinstallers"></a>**CoDeviceInstallers**  
包含有关在系统上注册的特定于类的共同安装程序的信息。

<a href="" id="deviceclasses"></a>**DeviceClasses**  
包含有关系统上的设备接口的信息。 每个[设备接口类](device-interface-classes.md)都有一个子项。

 

 





