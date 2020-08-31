---
title: 访问已安装设备接口的属性
description: 访问已安装设备接口的属性
ms.assetid: 4079DD59-878E-4b71-9815-543BA838C56D
keywords:
- 设备接口 WDK 设备安装，访问属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b7a2702f4bbdc90d1f2fe7227e2af3aadd21327
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096255"
---
# <a name="accessing-the-properties-of-installed-device-interfaces"></a>访问已安装设备接口的属性


若要发现在系统上注册的设备接口的属性，您不能通过直接访问注册表来打开、读取或写入设备接口子项。 与任何注册表项一样，在不同版本的 Windows 之间，密钥的位置、名称或格式可能会更改。

使用以下准则来安全地查询和修改设备接口的属性：

-   用户模式应用程序应遵循以下步骤：

    1.  使用 [**SetupDiOpenDeviceInterface**](/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfacea) 查找设备接口，并将其从其名称添加到集。

    2.  使用 [**SetupDiGetDeviceInterfaceDetail**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila) 检索设备接口的详细信息。

        可选的 *DeviceInfoData* 参数将接收注册了接口的设备的 [**SP_DEVINFO_DATA**](/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data) 元素。

    3.  使用持久性注册表存储作为设备接口类的自定义设置。 为此，请使用 [**SetupDiCreateDeviceInterfaceRegKey**](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfaceregkeya) (创建新的注册表项) 或 [**SetupDiOpenDeviceInterfaceRegKey**](/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey) (，以打开现有注册表项) 。

        若要保存自定义设置，请在创建或打开注册表项后使用 [RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543) 。

-   内核模式驱动程序应使用 [**IoOpenDeviceInterfaceRegistryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey) 来打开设备接口类的注册表项。

 

