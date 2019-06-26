---
title: 驱动程序文件中嵌入的签名
description: 驱动程序文件中嵌入的签名
ms.assetid: 21941c7b-4f9a-424c-9984-3048a53398b6
keywords:
- 嵌入式的签名 WDK 驱动程序签名
- 驱动程序签名 WDK，嵌入
- 签署驱动程序 WDK，嵌入
- 数字签名 WDK 嵌入
- 签名 WDK 嵌入
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 021949f7a3d1efac132fbcbcb92e4158ec05690e
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393436"
---
# <a name="embedded-signatures-in-a-driver-file"></a>驱动程序文件中嵌入的签名


在 64 位版本的 Windows Vista 和更高版本的 Windows 中，内核模式代码签名要求必须具有嵌入[软件发布者证书 (SPC)](software-publisher-certificate.md)签名。 不需要的驱动程序，不是引导启动驱动程序的嵌入式的签名。

**请注意**  Windows 10 桌面版 （主页、 专业版、 企业版和教育版） 和 Windows Server 2016 内核模式驱动程序必须进行签名的 Windows 硬件开发人员中心仪表板和 Windows 硬件开发人员中心仪表板需要使用 EV 证书。 有关这些更改的详细信息，请参阅[Windows 10 中的驱动程序签名更改](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)。

 

具有嵌入式的签名将保存在系统启动期间很长时间，因为系统加载程序以查找无需[编录文件](catalog-files.md)在系统启动驱动程序。 典型的计算机，运行 Windows Vista 或更高版本的 Windows，可能会在目录的根存储中具有很多不同的目录文件 ( *%系统 %\\CatRoot*)。 查找正确的目录文件，以验证驱动程序文件的指纹，则可能需要相当长的时间。

除了由内核模式代码签名策略强制执行的加载时间签名要求，插即用 (PnP) 设备安装还强制实施的安装时间签名要求。 若要符合[PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)Windows Vista 和更高版本的 Windows，[驱动程序包](driver-packages.md)即插即用设备必须具有签名的编录文件。

因为有选择性地包含在目录文件和嵌入签名中的指纹的缩略图中排除的驱动程序文件的签名部分目录文件的签名不妨碍嵌入式的签名。

使用驱动程序文件进行签名[SignTool](installing-a-catalog-file-by-using-signtool.md)工具。

 

 





