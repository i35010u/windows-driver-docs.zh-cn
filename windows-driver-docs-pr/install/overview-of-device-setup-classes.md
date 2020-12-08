---
title: 设备安装程序类概述
description: 设备安装程序类概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6bf7a0b5e049350ed4ccbf3714059318896ddfd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795451"
---
# <a name="overview-of-device-setup-classes"></a>设备安装程序类概述


为了便于设备安装，以相同方式设置和配置的设备将分组为一个设备安装程序类。 例如，将 SCSI 媒体转换器设备分组到 MediumChanger 设备安装程序类中。 设备安装程序类定义安装设备所涉及的类安装程序和类共同安装程序。

Microsoft 为大多数设备定义安装程序类。 IHV 和 OEM 可以定义新的设备安装程序类，但前提是现有类都不适用。 例如，照相机供应商不需要定义新的安装类，因为相机落在图像安装程序类下。 同样，不间断电源 (UPS) 设备位于电池类下。

有一个与每个设备安装程序类相关联的 GUID。 系统定义的安装程序类 Guid 是在 *Devguid* 中定义的，并且通常具有格式 GUID_DEVCLASS_ *Xxx* 格式的符号名称。

设备安装程序类 GUID 定义 **。 \\CurrentControlSet \\ Control \\ 类 \\**<em>ClassGuid</em>用于为标准安装程序类的任何特定设备创建新子项的注册表项。

 

 





