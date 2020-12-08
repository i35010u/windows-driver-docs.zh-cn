---
title: 设备和驱动程序的注册表树和项
description: 设备和驱动程序的注册表树和项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3188f152d615a36c7dcbc5286dece40268ad654c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808115"
---
# <a name="registry-trees-and-keys-for-devices-and-drivers"></a>设备和驱动程序的注册表树和项


操作系统、驱动程序和设备安装组件存储有关注册表中的驱动程序和设备的信息。 通常，驱动程序和设备安装组件应使用注册表来存储在系统重新启动时必须维护的数据。 有关驱动程序如何访问注册表信息的信息，请参阅 [使用驱动程序中的注册表](../kernel/registry-key-object-routines.md)。

注册表内容应始终被视为不受信任的可修改信息。 如果你的某个驱动程序组件将信息写入注册表，而另一个组件稍后读取它，则不会假设在此之后未修改该信息。 在从注册表中读取信息之后，驱动程序组件应始终在使用之前对其进行验证。

有关注册表的一般详细信息，请参阅 Microsoft Windows SDK 文档。

本部分包含以下主题，这些主题描述如何使用注册表项来存储有关驱动程序和设备的信息：

[设备和驱动程序的注册表树](overview-of-registry-trees-and-keys.md)

[RunOnce 注册表项](runonce-registry-key.md)

[DeviceOverrides 注册表项](deviceoverrides-registry-key.md)

驱动程序必须使用 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty) 或 [**IoOpenDeviceRegistryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)等系统例程访问注册表中即插即用 (PnP) 密钥。 用户模式安装组件应使用设备安装功能，如 [**SetupDiGetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya) 或 [**SetupDiOpenDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendevregkey)。 可以通过使用 [**Inf AddReg 指令**](inf-addreg-directive.md)从 INF 文件访问注册表。

**重要**  *驱动程序不能直接访问这些注册表树和密钥。* 本部分中的注册表信息讨论仅用于调试设备安装或配置问题。

 

