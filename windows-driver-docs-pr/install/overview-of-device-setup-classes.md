---
title: 设备安装程序类概述
description: 设备安装程序类概述
ms.assetid: 318ec3f4-f2c2-437c-a767-494ac240cb89
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 433dec1ec7f9de7b0113e04bdeabdce8472be9db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330232"
---
# <a name="overview-of-device-setup-classes"></a>设备安装程序类概述


若要简化设备安装，设备设置和配置相同的方式进行分组到设备安装程序类。 例如，SCSI 媒体更换器设备分为 MediumChanger 设备安装程序类。 设备安装程序类定义中安装设备的安装程序类和所涉及的类共同安装程序。

Microsoft 定义了适用于大多数设备安装程序类。 Ihv 和 Oem 可以定义新的设备安装程序类，但类仅如果没有，则现有应用。 例如，相机供应商无需定义新的安装程序类，因为照相机归入的映像安装程序类。 同样，不间断电源 (ups) 设备属于电池类。

没有与每个设备安装程序类关联的 GUID。 在中定义的系统定义的安装程序类 Guid *Devguid.h*并且通常具有符号名称的窗体 GUID_DEVCLASS_*Xxx*。

设备安装程序类 GUID 定义 **...\\CurrentControlSet\\控制\\类\\**<em>ClassGuid</em>在其下创建一个新子项的标准安装程序的任何特定设备的注册表项类。

 

 





