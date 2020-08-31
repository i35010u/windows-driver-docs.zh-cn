---
title: 64 位系统上的设备安装
description: 64 位系统上的设备安装
ms.assetid: 76d9bff7-6429-4d20-9790-a41ed2cb1bdd
keywords:
- 64位 WDK 设备安装
- 设备安装 WDK，64位系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32ccb26b7e53e87a3f025a3afa3d1a796dad3060
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096513"
---
# <a name="device-installations-on-64-bit-systems"></a>64 位系统上的设备安装





如果你的设备将安装在32位平台和64位平台上，则必须在创建 [驱动程序包](driver-packages.md)时执行以下步骤：

-   同时为所有内核模式驱动程序、 *设备安装应用程序*、 *类*安装程序和 *共同安装*程序提供32位和64位的编译。 有关详细信息，请参阅将 [驱动程序移植到64位 Windows](../kernel/porting-your-driver-to-64-bit-windows.md)。

-   提供一个或多个跨平台 INF 文件，这些文件使用 *修饰的 inf 节* 来控制特定于平台的安装行为。

如果要 [编写设备安装应用程序](writing-a-device-installation-application.md)，则32位版本必须是默认版本。 也就是说，32位版本应由 Microsoft Windows SDK 文档) 中描述的自动运行 (调用，使其在用户插入分发磁盘时自动启动。

32位版本的应用程序必须检查 [**UpdateDriverForPlugAndPlayDevices**](/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)返回的值。 如果返回值为 ERROR_IN_WOW64，则32位应用程序正在64位平台上执行，无法更新收件箱驱动程序。 相反，它必须调用 Windows SDK 文档) 中所述的 [**CreateProcess**](/windows/desktop/api/processthreadsapi/nf-processthreadsapi-createprocessa) (以启动应用程序的64位版本。 然后，64位版本可以调用 **UpdateDriverForPlugAndPlayDevices**，并指定 *FullInfPath* 参数以标识所有文件的64位版本的位置。

 

