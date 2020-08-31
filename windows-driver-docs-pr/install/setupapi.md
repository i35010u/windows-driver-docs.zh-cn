---
title: SetupAPI
description: SetupAPI
ms.assetid: aa12ec50-2842-4ddd-9fc5-84436d69ea7a
keywords:
- Setupapi.log WDK 设备安装，函数
- Setupapi.log 函数 WDK，关于 Setupapi.log 函数
- Setupapi.log 函数 WDK
- 设备设置 WDK 设备安装，Setupapi.log
- 设备安装 WDK，Setupapi.log
- 安装设备 WDK，Setupapi.log
- 函数 WDK Setupapi.log
- 设备安装 WDK，Setupapi.log
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21f126e8808905ef6cb200d99dfaf23e1a7e7c18
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096287"
---
# <a name="setupapi"></a>SetupAPI


 (Setupapi.log) 的安装应用程序编程接口是提供两组函数的系统组件：

-   [常规设置函数](using-general-setup-functions.md)

-   [设备安装功能](using-device-installation-functions.md)

设备安装软件可以使用这些功能在[*类安装*](writing-class-installers-and-co-installers.md)程序、[*共同安装*](writing-a-co-installer.md)[*程序和设备安装应用程序*](writing-a-device-installation-application.md)中执行自定义操作。

对于设备安装应用程序，驱动程序安装框架 (DIFx) 提供了一些高级工具，这些工具可抽象地即插即用 (PnP) 函数驱动程序和管理应用程序软件和驱动程序之间的关联。 如果 DIFx 工具提供安装应用程序为设备安装 PnP 驱动程序和应用程序软件所需的功能，则安装应用程序应使用 DIFx 工具，而不是直接调用 Setupapi.log 函数。 但是，通过在 [设备安装程序类](./overview-of-device-setup-classes.md)中执行设备的自定义操作或设备安装程序类中的所有设备，共同安装程序和类安装程序是 Microsoft Win32 dll，可帮助进行默认安装操作。 这些操作通常需要直接调用 Win32 函数和 Setupapi.log 函数。

本部分包含以下主题，其中提供了有关如何使用 Setupapi.log 提供的 [常规安装函数](using-general-setup-functions.md) 和 [设备安装功能](using-device-installation-functions.md) 的一般信息：

[使用常规设置函数](using-general-setup-functions.md)

[使用设备安装函数](using-device-installation-functions.md)

[SetupAPI 使用指南](guidelines-for-using-setupapi.md)

**注意**   本节仅介绍 Setupapi.log 中的部分安装函数。 有关此 API 的详细信息，请参阅 [设置 API](/windows/desktop/SetupApi/setup-api-portal) 。

 

 

