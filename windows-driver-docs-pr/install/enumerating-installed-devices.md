---
title: 枚举已安装的设备
description: 枚举已安装的设备
ms.assetid: 98EF9A16-6415-4778-BB5D-C0B7160C1509
keywords:
- 枚举安装的设备 WDK
- 已安装的设备 WDK，枚举
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ac3f98fc4a995439ef81d1fc233838b7e5da2c3
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717398"
---
# <a name="enumerating-installed-devices"></a>枚举已安装的设备


不应直接使用注册表项来枚举设备。 注册表项不包含枚举系统上已安装设备所需的信息。 此信息（如设备实际是否存在，或者是否为虚拟设备 (未接通) 的设备）由 [即插即用 (PnP) 管理器](pnp-manager.md)保留。 PnP 管理器还会对注册表信息执行其他筛选。

若要安全地枚举安装的设备，请执行以下步骤：

1.  使用 [**SetupDiGetClassDevs**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsw) 或 [**SetupDiGetClassDevsEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsexa) 检索属于指定设备安装程序类的一组设备的信息。 若要仅检索系统中存在的设备的信息，请在 *Flags* 参数中设置 DIGCF_PRESENT。

2.  使用 [**SetupDiEnumDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinfo) 枚举集中的设备。

3.  使用 [**SetupDiGetDeviceInstanceId**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinstanceida) 检索 [)  (id 的唯一设备实例标识符 ](device-instance-ids.md)。

 

