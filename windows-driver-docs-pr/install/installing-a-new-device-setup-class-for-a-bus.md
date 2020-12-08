---
title: 为总线安装新的设备安装程序类
description: 为总线安装新的设备安装程序类
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef3bbaa982f7b1cc275d420399e6980488c98ed9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840341"
---
# <a name="installing-a-new-device-setup-class-for-a-bus"></a>为总线安装新的设备安装程序类


如果新总线支持的设备的功能明显不同于属于现有 [设备安装程序类](./overview-of-device-setup-classes.md)的设备提供的功能，则应为总线安装新的设备安装程序类。 有关帮助您确定是否安装新设备安装程序类的详细信息，请参阅 [创建新的设备安装程序类](creating-a-new-device-setup-class.md)。

若要为总线安装新的设备安装程序类，请在 [**Inf 版本部分**](inf-version-section.md)中设置相关指令，包括 [**inf ClassInstall32 部分**](inf-classinstall32-section.md)，并根据需要包括 inf Class32 部分引用的其他部分。

以下带批注的示例说明了安装 [设备安装程序类](./overview-of-device-setup-classes.md)需要包含的基本 INF 文件条目。 有关设备安装程序类的可能的配置设置的信息，请参阅 [**INF ClassInstall32 部分**](inf-classinstall32-section.md)。

```cpp
[Version]
signature="$CHICAGO$"
; Specify a unique class name that identifies the manufacturer and the bus type
Class=%AbcSuperBus%

; Specify a unique GUID that identifies the device setup class
ClassGUID={17ed6609-9bc8-44ca-8548-abb79b13781b}

; Identify the provider of the INF file
Provider=%AbcCorp%

; Specify the version of the device driver
DriverVer=01/01/2007,1.0.0.0 

[ClassInstall32]
; Reference an AddReg directive that specifies class properties
Addreg=AbcSuperBusClassReg 

[AbcSuperBusClassReg]
; Specify the properties of the device setup class
HKR,,,,%AbcSuperBus%
HKR,,Icon,,-19
HKR,,NoInstallClass,,1
. . .
. . .
[Strings] 
AbcCorp="Abc Corporation"
AbcSuperBus="Abc Corporation Super Bus Controller"
```

 

