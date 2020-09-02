---
title: 安装 IEEE 1394 设备驱动程序
description: 安装 IEEE 1394 设备驱动程序
ms.assetid: 3f99bec7-e657-4de7-bce4-36a779cc0442
keywords:
- IEEE 1394 WDK 总线，驱动程序安装
- 1394 WDK 总线，驱动程序安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8b2c61dee7d73d6db33949be7a5418ef0a7ebbd
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382217"
---
# <a name="installing-ieee-1394-device-drivers"></a>安装 IEEE 1394 设备驱动程序





本部分提供特定于 Microsoft Windows 2000 和更高版本操作系统中的 IEEE 1394 设备驱动程序的安装信息。

提供其自己的 IEEE 1394 设备驱动程序的供应商应该使该驱动程序成为驱动程序 INF 文件的 " [**Inf 版本" 部分**](../install/inf-version-section.md) 中基本安装程序类的成员。 例如：

```cpp
[Version]
Signature="$WINDOWS NT$"
Class = Base
```

安装 IEEE 1394 设备驱动程序没有其他特殊要求。

有关 Windows 2000 及更高版本操作系统中的设备安装的常规信息，请参阅 [设备安装概述](../install/overview-of-device-and-driver-installation.md)。

 

