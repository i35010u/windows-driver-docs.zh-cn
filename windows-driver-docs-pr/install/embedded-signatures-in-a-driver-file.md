---
title: 驱动程序文件中嵌入的签名
description: 驱动程序文件中嵌入的签名
ms.assetid: 21941c7b-4f9a-424c-9984-3048a53398b6
keywords:
- 嵌入签名 WDK 驱动程序签名
- 驱动程序签名 WDK，embedded
- 对驱动程序进行签名 WDK，embedded
- 数字签名 WDK，embedded
- 签名 WDK，embedded
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abefc35277c7657c6271c49aa258ee634e5e86fc
ms.sourcegitcommit: e1f02bc9a982eefa1e326c95d3aca5ecc68581ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73721621"
---
# <a name="embedded-signatures-in-a-driver-file"></a>驱动程序文件中嵌入的签名


在 Windows Vista 和更高版本的 windows 的64位版本中，内核模式代码签名要求必须有嵌入式[软件发行者证书（SPC）](software-publisher-certificate.md)签名。 不是启动驱动程序驱动程序的驱动程序不需要嵌入签名。

> [!NOTE]
> 适用于桌面版的 windows 10 （家庭版、专业版、企业版和教育版）和 Windows Server 2016 内核模式驱动程序必须由 Windows 硬件开发人员中心仪表板签名，这需要 EV 证书。 有关这些更改的详细信息，请参阅[Windows 10 中的驱动程序签名更改](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/Driver-Signing-changes-in-Windows-10-version-1607/ba-p/364894)。

 

由于不需要系统加载程序在系统启动时找到驱动程序的[编录文件](catalog-files.md)，因此在系统启动期间嵌入的签名会节省大量时间。 典型的计算机可能在目录根存储区（ *% System%\\CatRoot*）中有很多不同的目录文件。 定位正确的目录文件以验证驱动程序文件的指纹可能需要花费大量时间。

除了由内核模式代码签名策略强制执行的加载时间签名要求外，即插即用（PnP）设备还会强制执行安装时签名要求。 为了符合 Windows Vista 和更高版本的 Windows 的[pnp 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)，pnp 设备的[驱动程序包](driver-packages.md)必须具有签名的目录文件。

嵌入的签名不会干扰目录文件的签名，因为目录文件中包含的指纹和嵌入签名中的指纹可以选择性地排除驱动程序文件的签名部分。

驱动程序文件通过使用[SignTool](installing-a-catalog-file-by-using-signtool.md)工具进行签名。

 

 





