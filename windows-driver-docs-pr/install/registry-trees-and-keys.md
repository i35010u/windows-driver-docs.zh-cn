---
title: 设备和驱动程序的注册表树和项
description: 设备和驱动程序的注册表树和项
ms.assetid: 8f6ac7c1-f31a-4d14-8ba7-b432615db073
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0ffef196f84300f7f5e4002fd24b409d0c611ba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387321"
---
# <a name="registry-trees-and-keys-for-devices-and-drivers"></a>设备和驱动程序的注册表树和项


操作系统、 驱动程序和设备安装组件在注册表中存储有关驱动程序和设备信息。 一般情况下，驱动程序和设备安装组件应使用注册表来存储必须在重启后的系统维护的数据。 有关驱动程序访问注册表信息的方式的信息，请参阅[使用到的驱动程序注册表](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-the-registry-in-a-driver)。

注册表内容始终应视为不受信任的、 可修改的信息。 如果其中一个驱动程序组件的信息写入注册表和另一个组件读取更高版本，不要假定，已在此期间不被修改的信息。 读取注册表中的信息之后, 驱动程序组件应始终验证信息，然后使用它。

有关注册表的详细信息的一般情况下，请参阅 Microsoft Windows SDK 文档。

本部分包含以下主题介绍使用注册表项来存储有关驱动程序和设备信息：

[设备和驱动程序的注册表树](overview-of-registry-trees-and-keys.md)

[RunOnce 注册表项](runonce-registry-key.md)

[DeviceOverrides 注册表项](deviceoverrides-registry-key.md)

驱动程序必须访问插即用 (PnP) 密钥使用系统例程，如注册表中的[ **IoGetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)或[ **IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey). 用户模式下安装组件应使用设备安装函数如[ **SetupDiGetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)或[ **SetupDiOpenDevRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey). 可以通过使用从 INF 文件访问注册表[ **INF AddReg 指令**](inf-addreg-directive.md)。

**重要**  *驱动程序不能访问这些注册表树和密钥直接。* 本部分中的注册表信息的这一讨论仅适用于调试设备安装或配置问题。

 

 

 





