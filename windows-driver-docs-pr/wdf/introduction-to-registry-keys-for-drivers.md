---
title: 介绍驱动程序的注册表项
description: 介绍驱动程序的注册表项
ms.assetid: ec1a21db-1a31-4041-941d-31156884ffae
keywords:
- 注册表 WDK KMDF
- 注册表项对象 WDK KMDF
- 基于框架的驱动程序 WDK KMDF、 注册表
- 内核模式驱动程序 WDK KMDF、 注册表
- KMDF WDK 注册表
- 内核模式驱动程序框架 WDK、 注册表
- 参数项 WDK KMDF
- 软件密钥 WDK KMDF
- 驱动程序键 WDK KMDF
- 硬件密钥 WDK KMDF
- 密钥 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b0eb09c81628c1e9072f1e062dc1dfb30f882af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543931"
---
# <a name="introduction-to-registry-keys-for-drivers"></a>介绍驱动程序的注册表项


驱动程序通常使用一系列系统定义的注册表项来存储或访问特定于驱动程序或特定于设备的信息。 您的驱动程序可能会访问以下注册表项：

-   **参数**密钥

    在驱动程序**参数**键可以包含您的驱动程序的配置信息。 内核模式驱动程序框架 (KMDF) 的驱动程序，此密钥位于[ **HKLM\\系统\\CurrentControlSet\\Services** ](https://msdn.microsoft.com/library/windows/hardware/ff546188)树中，在驱动程序的下服务名称。 对于用户模式驱动程序框架 (UMDF) 驱动程序，此密钥位于**HKLM\\软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\服务**树中，在驱动程序的服务名称下。 驱动程序的子项始终使用驱动程序的服务名称，即使该驱动程序二进制文件的文件名不同于服务名称。

    当系统调用您的驱动程序[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff540807)例程，该驱动程序将路径传递到驱动程序的**Services**树。 您的驱动程序必须将传递到此路径[ **WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)。 随后，该驱动程序可以通过调用获取的路径[ **WdfDriverGetRegistryPath**](https://msdn.microsoft.com/library/windows/hardware/ff547187)，并驱动程序可以打开其**参数**密钥通过调用[ **WdfDriverOpenParametersRegistryKey**](https://msdn.microsoft.com/library/windows/hardware/ff547202)。

    有关详细信息**参数**密钥，请参阅[HKLM\\系统\\CurrentControlSet\\服务树](https://msdn.microsoft.com/library/windows/hardware/ff546188)。

-   软件密钥

    也称为驱动程序的软件密钥及其*驱动程序键*因为注册表包含软件密钥的每个驱动程序。 注册表包含的所有设备类列表和每个驱动程序软件密钥驻留在其设备类项下。 系统将存储在其软件项下每个驱动程序有关的信息。

    您的驱动程序可以调用[ **WdfFdoInitOpenRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff547249)并[ **WdfDeviceOpenRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff546804)以打开其软件密钥。

    有关软件密钥的详细信息，请参阅[HKLM\\系统\\CurrentControlSet\\控件树](https://msdn.microsoft.com/library/windows/hardware/ff546165)。

-   硬件密钥

    当驱动程序堆栈可以通知插即用 (PnP) 管理器设备连接到系统时，即插即用管理器创建设备的硬件密钥。 此密钥也称为*设备密钥*。 PnP 管理器存储设备的硬件项下的每个设备的唯一标识信息。

    您的驱动程序可以调用[ **WdfFdoInitOpenRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff547249)并[ **WdfDeviceOpenRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff546804)打开设备的硬件密钥。

    有关硬件密钥的详细信息，请参阅[HKLM\\系统\\CurrentControlSet\\枚举树](https://msdn.microsoft.com/library/windows/hardware/ff546173)。

驱动程序的 INF 文件可以包含[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)设置注册表值。 INF 文件通常使用[ **INF DDInstall.HW 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547330)设置下设备的硬件密钥的信息。

若要确定驱动程序类型是否需要存储特定的注册表项下的信息，请参阅本文档讨论驱动程序的设备类型使用的目录的部分。

有关驱动程序的注册表项的详细信息，请参阅：

-   [注册表树和密钥概述](https://msdn.microsoft.com/library/windows/hardware/ff549538)

-   [使用到的驱动程序注册表](https://msdn.microsoft.com/library/windows/hardware/ff565537)

 

 





