---
title: 为总线安装新的设备安装程序类
description: 为总线安装新的设备安装程序类
ms.assetid: a94899b6-02e0-4181-bb14-5552806a8c9e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 663fb8f1155aaa98c567d3d98673192d1927aee9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364975"
---
# <a name="installing-a-new-device-setup-class-for-a-bus"></a>为总线安装新的设备安装程序类


如果新总线支持的功能有很大区别属于现有的设备提供的功能的设备[设备安装程序类](device-setup-classes.md)，应安装新的设备安装程序类为总线。 有关可帮助您确定是否要安装新的设备安装程序类的详细信息，请参阅[创建新的设备安装程序类](creating-a-new-device-setup-class.md)。

若要安装新的设备安装程序类为总线，在中设置相关的指令[ **INF 版本部分**](inf-version-section.md)，包括[ **INF ClassInstall32 部分**](inf-classinstall32-section.md)，并包含其他部分中，根据需要 INF Class32 部分引用的。

以下带批注的示例说明了您需要包含要安装的基本 INF 文件条目[设备安装程序类](device-setup-classes.md)。 有关可能的配置设置的设备安装程序类的信息，请参阅[ **INF ClassInstall32 部分**](inf-classinstall32-section.md)。

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

 

 





