---
title: 枚举已安装的设备
description: 枚举已安装的设备
keywords:
- 枚举安装的设备 WDK
- 已安装的设备 WDK，枚举
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3daffe9f2e5d4fe070c414cb52ce672968e0001
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813155"
---
# <a name="enumerating-installed-devices"></a>枚举已安装的设备


不应直接使用注册表项来枚举设备。 注册表项不包含枚举系统上已安装设备所需的信息。 此信息（如设备实际是否存在，或者是否为虚拟设备 (未接通) 的设备）由 [即插即用 (PnP) 管理器](pnp-manager.md)保留。 PnP 管理器还会对注册表信息执行其他筛选。

若要安全地枚举安装的设备，请执行以下步骤：

1.  使用 [**SetupDiGetClassDevs**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsw) 或 [**SetupDiGetClassDevsEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsexa) 检索属于指定设备安装程序类的一组设备的信息。 若要仅检索系统中存在的设备的信息，请在 *Flags* 参数中设置 DIGCF_PRESENT。

2.  使用 [**SetupDiEnumDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinfo) 枚举集中的设备。

3.  使用 [**SetupDiGetDeviceInstanceId**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinstanceida) 检索 [)  (id 的唯一设备实例标识符](device-instance-ids.md)。

 

