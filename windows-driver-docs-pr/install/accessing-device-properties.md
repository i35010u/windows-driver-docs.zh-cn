---
title: 访问设备属性
description: 访问设备属性
ms.assetid: 7D3F3164-E530-49fb-BCCD-9C024543FA95
keywords:
- 设备属性 WDK 设备安装，访问
- 访问设备属性 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 309e9583b3880040798ace2ea43d7bd10e4b5893
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385017"
---
# <a name="accessing-device-properties"></a>访问设备属性


您不能发现或更改[设备属性](device-properties.md)通过直接访问注册表项。 注册表项不包含所需的信息发现或更改设备属性。 此外，位置、 格式和含义的这些密钥的 Windows 不同版本之间可能会更改。

[SetupAPI](setupapi.md)函数提供一致的行为和强制执行访问权限来保护设备属性。 从 Windows Vista 开始，具有受限写入访问权限的设备属性还具有读取访问权限限制。

若要安全地访问设备属性，请遵循以下准则：

-   用户模式应用程序，请执行以下步骤：

    1.  从 Windows Vista 开始，使用[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)以检索设备属性，并使用[ **SetupDiSetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)DEVPKEY_Xxx 属性代码来设置设备的属性。

        在 Windows Vista 和更高版本的 Windows 设备实例属性的详细信息，请参阅[访问设备实例属性 （Windows Vista 和更高版本）](accessing-device-instance-properties--windows-vista-and-later-.md)。

        **请注意**  从 Windows Vista 开始，某些设备属性保留了操作系统。 有关详细信息，请参阅[修改设备属性](modifying-device-properties.md)。

    2.  在 Windows 2000，Windows XP 和 Windows Server 2003 上，使用[ **SetupDiGetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)以检索设备属性，并使用[ **SetupDiSetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya) SPDRP_Xxx 属性代码来设置设备的属性。

        在 Windows 2000，Windows XP 和 Windows Server 2003 设备实例属性的详细信息，请参阅[访问设备实例 SPDRP_Xxx 属性](accessing-device-instance-spdrp-xxx-properties.md)。

    3.  为自定义设置的实际存在的设备的和不在注册表中使用持久性存储区。 在这种情况下，必须创建您自己的注册表项和值集。 若要执行此操作，请使用**SetupDiCreateDevRegKey** (DIREG_DEV) 或*软件密钥*(DIREG_DRV) 设备。

        **请注意**  硬件密钥保留在注册表中，直到卸载设备。 软件密钥可以移动或清除[设备安装组件](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))驱动程序升级过程

        若要保存的自定义设置，请使用[RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543)后创建的注册表项或将其打开。

-   有关内核模式驱动程序，使用[ **IoGetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)以访问设备的属性。

 

 





