---
title: 安装更换器微型类驱动程序
description: 安装更换器微型类驱动程序
ms.assetid: 923e1128-bacc-450b-b250-bc666951965d
keywords:
- 更换器驱动程序 WDK 存储，miniclass 驱动程序
- 存储更换器驱动程序 WDK，miniclass 驱动程序
- miniclass 驱动程序 WDK 换带机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 606f298e39fe76f31f18f7e8ce57abcff1b66f65
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385228"
---
# <a name="installing-changer-miniclass-drivers"></a>安装更换器微型类驱动程序


## <span id="ddk_installing_changer_miniclass_drivers_kg"></span><span id="DDK_INSTALLING_CHANGER_MINICLASS_DRIVERS_KG"></span>


本部分提供特定于 Windows 2000 和更高版本操作系统中换带机 miniclass 驱动程序的安装信息。

供应商提供其自己的控制器微型驱动程序应使该微型驱动程序中的 MediumChanger 安装程序类的成员[ **INF 版本部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)的驱动程序的 INF 文件。 例如：

```cpp
[version]
Signature="$WINDOWS NT$"
Class=MediumChanger
ClassGuid={CE5939AE-EBDE-11d0-B181-0000F8753EC4}
```

不没有与安装换带机 miniclass 驱动程序相关联的任何其他特殊的要求。

有关安装的详细信息，请参阅随附包含 Windows Driver Kit (WDK) 中的媒体更换器示例的 INF 文件。

有关在 Windows 2000 和更高版本操作系统的设备安装的常规信息，请参阅[设备安装概述](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)。

 

 




