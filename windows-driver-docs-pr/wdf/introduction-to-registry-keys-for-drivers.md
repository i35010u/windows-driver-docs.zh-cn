---
title: 驱动程序的注册表项简介
description: 驱动程序的注册表项简介
keywords:
- 注册表 WDK KMDF
- 注册表-密钥对象 WDK KMDF
- 基于框架的驱动程序 WDK KMDF，注册表
- 内核模式驱动程序 WDK KMDF、注册表
- KMDF WDK，注册表
- Kernel-Mode Driver Framework WDK，注册表
- 参数密钥 WDK KMDF
- 软件密钥 WDK KMDF
- 驱动程序密钥 WDK KMDF
- 硬件密钥 WDK KMDF
- 密钥 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c192bce29594a83aa7df286122ecae1abc3c9a7
ms.sourcegitcommit: a7e7fb05f2f68d09bb0892c99a65dcb542efc11a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97860611"
---
# <a name="introduction-to-registry-keys-for-drivers"></a>驱动程序的注册表项简介


驱动程序通常使用一组系统定义的注册表项来存储或访问驱动程序特定的信息或特定于设备的信息。 你的驱动程序可能会访问以下注册表项：

-   **参数** 键

    驱动程序的 **参数** 密钥可包含驱动程序的配置信息，并可通过调用 [**WdfDriverOpenParametersRegistryKey**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriveropenparametersregistrykey)进行访问。 对于 Kernel-Mode Driver Framework (KMDF) 驱动程序，此密钥位于驱动程序的相应 **服务** 树中。 对于 User-Mode Driver Framework (UMDF) 驱动程序，此密钥位于驱动程序服务名称下的 **HKLM \\ SOFTWARE \\ Microsoft \\ Windows NT \\ CurrentVersion \\ WUDF \\ Services** 树中。 驱动程序的子项始终使用驱动程序的服务名称，即使驱动程序二进制文件的文件名不同于服务名称也是如此。

    当系统调用驱动程序的 [**DriverEntry**](./driverentry-for-kmdf-drivers.md) 例程时，它会将驱动程序的路径传递到相应 **服务** 树中的驱动程序的密钥。 你的驱动程序必须将此路径传递给 [**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)。 随后，驱动程序可以通过调用 [**WdfDriverGetRegistryPath**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivergetregistrypath)来获取路径。

-   软件密钥

    驱动程序的软件密钥也称为 " *驱动程序密钥*"。 系统在其软件密钥下存储有关每个驱动程序的信息。

    你的驱动程序可以调用 [**WdfFdoInitOpenRegistryKey**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey) 和 [**WdfDeviceOpenRegistryKey**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceopenregistrykey) 以打开设备的软件密钥。

    驱动程序的 INF 文件可包含使用 [**Inf DDInstall 部分**](../install/inf-ddinstall-section.md)在软件密钥下设置注册表值的 [**inf AddReg 指令**](../install/inf-addreg-directive.md)。

-   硬件密钥

    当驱动程序堆栈通知即插即用设备连接到系统 (PnP) 管理器时，PnP 管理器将为该设备创建一个硬件密钥。 此密钥也称为 *设备密钥*。 与硬件 (相关的设置（如中断设置) 可通过驱动程序存储在此处。

    你的驱动程序可以调用 [**WdfFdoInitOpenRegistryKey**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey) 和 [**WdfDeviceOpenRegistryKey**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceopenregistrykey) 以打开设备的硬件密钥。

    驱动程序的 INF 文件可包含使用 [**Inf DDInstall 部分**](../install/inf-ddinstall-hw-section.md)在硬件密钥下设置注册表值的 [**inf AddReg 指令**](../install/inf-addreg-directive.md)。

若要确定你的驱动程序类型是否要求你将信息存储在特定的注册表项下，请参阅本文档中的部分，其中介绍了如何使用目录讨论驱动程序的设备类型。

有关驱动程序的注册表项的详细信息，请参阅：

-   [在驱动程序中使用注册表](../kernel/registry-key-object-routines.md)
