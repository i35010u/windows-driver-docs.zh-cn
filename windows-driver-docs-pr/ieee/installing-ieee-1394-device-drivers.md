---
title: 安装 IEEE 1394 设备驱动程序
description: 安装 IEEE 1394 设备驱动程序
ms.assetid: 3f99bec7-e657-4de7-bce4-36a779cc0442
keywords:
- IEEE 1394 WDK 总线，驱动程序安装
- 1394 WDK 总线，驱动程序安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37bdefa6af9a51303dd10f8c9ea930cce95e0022
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385768"
---
# <a name="installing-ieee-1394-device-drivers"></a>安装 IEEE 1394 设备驱动程序





本部分提供特定于 Microsoft Windows 2000 和更高版本操作系统中的 IEEE 1394 设备驱动程序的安装信息。

供应商提供其自己的 IEEE 1394 设备驱动程序应使该驱动程序中的基本安装程序类的成员[ **INF 版本部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)的驱动程序的 INF 文件。 例如：

```cpp
[Version]
Signature="$WINDOWS NT$"
Class = Base
```

不没有与安装 IEEE 1394 设备驱动程序相关联的任何其他特殊的要求。

有关在 Windows 2000 和更高版本操作系统的设备安装的常规信息，请参阅[设备安装概述](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)。

 

 




