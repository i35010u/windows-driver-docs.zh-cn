---
title: 访问设备属性
description: 访问设备属性
ms.assetid: 7D3F3164-E530-49fb-BCCD-9C024543FA95
keywords:
- 设备属性 WDK 设备安装，访问
- 访问设备属性 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76e6e17e14a5c3e7ebb102bc5c88d6b583d9eb45
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097349"
---
# <a name="accessing-device-properties"></a>访问设备属性


不能通过直接访问注册表项来发现或更改 [设备属性](device-properties.md) 。 注册表项不包含发现或更改设备属性所需的信息。 此外，这些密钥的位置、格式和含义可能在不同版本的 Windows 之间发生变化。

[Setupapi.log](setupapi.md)函数提供一致的行为，并强制访问权限以保护设备属性。 从 Windows Vista 开始，具有受限写入访问权限的设备属性也具有受限的读取访问权限。

若要安全访问设备属性，请遵循以下准则：

-   对于用户模式应用程序，请执行以下步骤：

    1.  从 Windows Vista 开始，使用 [**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 检索设备属性，并使用具有 DEVPKEY_Xxx 属性代码的 [**SetupDiSetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw) 设置设备属性。

        有关 Windows Vista 和更高版本的 Windows 上的设备实例属性的详细信息，请参阅 [ (Windows vista 和更高版本) 访问设备实例属性 ](accessing-device-instance-properties--windows-vista-and-later-.md)。

        **注意**   从 Windows Vista 开始，某些设备属性由操作系统保留。 有关详细信息，请参阅 [修改设备属性](modifying-device-properties.md)。

    2.  在 Windows 2000、Windows XP 和 Windows Server 2003 上，使用 [**SetupDiGetDeviceRegistryProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw) 检索设备属性，并使用具有 SPDRP_Xxx 属性代码的 [**SetupDiSetDeviceRegistryProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya) 设置设备属性。

        有关 Windows 2000、Windows XP 和 Windows Server 2003 上的设备实例属性的详细信息，请参阅 [SPDRP_Xxx 属性访问设备实例](accessing-device-instance-spdrp-xxx-properties.md)。

    3.  在注册表中使用持久性存储，用于实际存在的设备的自定义设置和不是这些设置的设备。 在这种情况下，必须创建自己的注册表项和值集。 为此，请使用 **SetupDiCreateDevRegKey** (DIREG_DEV) 或 *软件密钥* (设备的 DIREG_DRV) 。

        **注意**   在卸载设备之前，硬件密钥会一直保存在注册表中。 [设备安装组件](/previous-versions/ff541277(v=vs.85))在驱动程序升级过程中可以移动或清除软件密钥

        若要保存自定义设置，请在创建或打开注册表项后使用 [RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543) 。

-   对于内核模式驱动程序，请使用 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty) 访问设备属性。

 

