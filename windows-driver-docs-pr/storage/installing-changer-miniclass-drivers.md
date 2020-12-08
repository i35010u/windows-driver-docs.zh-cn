---
title: 安装更换器微型类驱动程序
description: 安装更换器微型类驱动程序
keywords:
- 转换器驱动程序 WDK 存储，miniclass 驱动程序
- 存储更换器驱动程序 WDK、miniclass 驱动程序
- miniclass 驱动程序 WDK 转换器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62febcbec5c5e0951f15301f722a3bf9562b1dd0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804463"
---
# <a name="installing-changer-miniclass-drivers"></a>安装更换器微型类驱动程序


## <span id="ddk_installing_changer_miniclass_drivers_kg"></span><span id="DDK_INSTALLING_CHANGER_MINICLASS_DRIVERS_KG"></span>


本部分提供特定于在 Windows 2000 和更高版本的操作系统中更换 miniclass 驱动程序的安装信息。

提供自己的控制器微型驱动程序的供应商应该使该微型驱动程序成为驱动程序 INF 文件的 [**Inf 版本部分**](../install/inf-version-section.md) 中 MediumChanger 安装程序类的成员。 例如：

```cpp
[version]
Signature="$WINDOWS NT$"
Class=MediumChanger
ClassGuid={CE5939AE-EBDE-11d0-B181-0000F8753EC4}
```

除了安装 miniclass 驱动程序以外，没有其他特殊要求。

有关更多安装信息，请参阅随 Windows 驱动程序工具包中包含的媒体更换器示例一起提供的 INF 文件 (WDK) 。

有关 Windows 2000 及更高版本操作系统中的设备安装的常规信息，请参阅 [设备安装概述](../install/overview-of-device-and-driver-installation.md)。

 

