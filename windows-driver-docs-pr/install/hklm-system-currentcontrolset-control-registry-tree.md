---
title: HKLM\SYSTEM\CurrentControlSet\Control 注册表树
description: HKLM\SYSTEM\CurrentControlSet\Control 注册表树包含用于控制系统启动和设备配置的某些方面的信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: feafab7c9225efaa08dcb2efb509c36babc361f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791753"
---
# <a name="hklmsystemcurrentcontrolsetcontrol-registry-tree"></a>HKLM \\ 系统 \\ CurrentControlSet \\ 控制注册表树





**HKLM \\ system \\ CurrentControlSet \\ Control** 注册表树包含用于控制系统启动和设备配置的某些方面的信息。 以下子项特别感兴趣：

<a href="" id="class"></a>**班级**  
包含有关系统上的 [设备安装程序类](./overview-of-device-setup-classes.md) 的信息。 使用安装程序类的 GUID 命名的每个类都有一个子项。 每个子项都包含有关安装程序类的信息，如类安装程序 (如果有一个) 、已注册的顶级筛选器驱动程序和已注册的类低筛选器驱动程序。

<a href="" id="codeviceinstallers"></a>**CoDeviceInstallers**  
包含有关在系统上注册的特定于类的共同安装程序的信息。

<a href="" id="deviceclasses"></a>**DeviceClasses**  
包含有关系统上的设备接口的信息。 每个 [设备接口类](./overview-of-device-interface-classes.md)都有一个子项。

 

