---
title: 枚举已安装的设备
description: 枚举已安装的设备
ms.assetid: 98EF9A16-6415-4778-BB5D-C0B7160C1509
keywords:
- 枚举已安装的设备 WDK
- 安装的设备 WDK，枚举
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 817033cd9b6f49b01e36cb408f6c527dd0d969ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379471"
---
# <a name="enumerating-installed-devices"></a>枚举已安装的设备


不应直接使用注册表项来枚举设备。 注册表项不包含所需的信息，以枚举在系统上的已安装的设备。 此信息，例如设备是否真的存在还是虚拟设备 （一种未插入），由[插即用 (PnP) 管理器](pnp-manager.md)。 PnP 管理器还执行其他筛选的注册表信息。

若要安全地枚举已安装的设备，请执行以下步骤：

1.  使用[ **SetupDiGetClassDevs** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)或[ **SetupDiGetClassDevsEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa)检索一组属于指定的设备信息设备安装程序类。 若要检索仅适用于系统中存在的设备的信息，请在中设置 DIGCF_PRESENT*标志*参数。

2.  使用[ **SetupDiEnumDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo)要枚举一组中的设备。

3.  使用[ **SetupDiGetDeviceInstanceId** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstanceida)检索唯一[设备实例标识符 (Id)](device-instance-ids.md)。

 

 





