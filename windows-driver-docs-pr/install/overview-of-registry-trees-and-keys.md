---
title: 设备和驱动程序的注册表树
description: 设备和驱动程序的注册表树
ms.assetid: 74dc1889-26a9-47ba-8c8d-3cd6ed95cb68
keywords:
- 硬件密钥 WDK 设备安装
- 注册表 WDK 设备安装
- 软件密钥 WDK 设备安装
- 设备安装 WDK、 注册表
- 安装设备 WDK、 注册表
- 设备安装程序 WDK 设备安装、 注册表
- 调试设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c46bd37a7562cbcd78bda72a402bf3d4880ad46
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330221"
---
# <a name="registry-trees-for-devices-and-drivers"></a>设备和驱动程序的注册表树





特定驱动程序编写人员感兴趣的是在注册表中的以下树 (其中**HKLM**表示**HKEY_LOCAL_MACHINE**):

-   [HKLM\\系统\\CurrentControlSet\\服务注册表树](hklm-system-currentcontrolset-services-registry-tree.md)

-   [HKLM\\系统\\CurrentControlSet\\控制注册表树](hklm-system-currentcontrolset-control-registry-tree.md)

-   [HKLM\\系统\\CurrentControlSet\\枚举注册表树](hklm-system-currentcontrolset-enum-registry-tree.md)

-   [HKLM\\系统\\CurrentControlSet\\HardwareProfiles 注册表树](hklm-system-currentcontrolset-hardwareprofiles-registry-tree.md)

有关从 WDF （KMDF 或 UMDF） 驱动程序访问注册表项的信息，请参阅[简介驱动程序的注册表项](../wdf/introduction-to-registry-keys-for-drivers.md)。

**请注意**  下的项**HKLM\\系统\\CurrentControlSet**是安全的位置来保留对您的驱动程序都很重要，因为数据存储在系统配置单元中的数据。 系统将额外的预防措施来保护系统配置单元 （例如，多个副本保留）。

 

 

 





