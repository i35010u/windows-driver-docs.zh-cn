---
title: SetupAPI
description: SetupAPI
ms.assetid: aa12ec50-2842-4ddd-9fc5-84436d69ea7a
keywords:
- SetupAPI WDK 设备安装函数
- 安装程序 Api 函数 WDK，有关安装程序 Api 函数
- 安装程序 Api 函数 WDK
- 设备安装程序 WDK 设备安装，安装程序 Api
- 设备安装 WDK，安装程序 Api
- 安装设备 WDK，安装程序 Api
- WDK SetupAPI 函数
- 设备安装 WDK，安装程序 Api
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c8557f28c42be16c703f4b4e256e5c4b50c6c21
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348645"
---
# <a name="setupapi"></a>SetupAPI


安装程序应用程序编程接口 (安装程序 Api) 是提供两组函数的系统组件：

-   [常规设置函数](using-general-setup-functions.md)

-   [设备安装函数](using-device-installation-functions.md)

设备安装软件可以使用这些函数执行中的自定义操作[*类的安装程序*](writing-class-installers-and-co-installers.md)， [*共同安装程序*](writing-a-co-installer.md)，并[*设备安装应用程序*](writing-a-device-installation-application.md)。

对于设备安装应用程序，驱动程序安装框架 (DIFx) 提供了抽象安装插即用 (PnP) 功能的驱动程序和管理应用程序软件之间的关联的低级别 SetupAPI 操作的高级工具和驱动程序。 如果 DIFx 工具提供了安装应用程序需安装即插即用驱动程序和设备的应用程序软件的功能，安装应用程序应使用 DIFx 工具而不是直接调用安装程序 Api 函数。 但是，共同安装程序和类安装程序是帮助通过执行自定义操作用于设备还是中的所有设备的默认安装操作的 Microsoft Win32 Dll[设备安装程序类](device-setup-classes.md)。 这些操作通常需要直接调用 Win32 函数和安装程序 Api 函数。

本部分包含以下主题，它们提供有关如何使用的一般信息[常规安装函数](using-general-setup-functions.md)并[设备安装函数](using-device-installation-functions.md)提供的安装程序 Api:

[使用通用安装程序函数](using-general-setup-functions.md)

[使用设备安装函数](using-device-installation-functions.md)

[典型的安装程序 Api 使用情况](typical-setupapi-usage.md)

[使用 SetupAPI 的准则](guidelines-for-using-setupapi.md)

**请注意**  本部分介绍了安装程序 Api 中的安装程序函数的一个子集。 有关此 API 的详细信息，请参阅[安装程序 API](https://docs.microsoft.com/windows/desktop/SetupApi/setup-api-portal) 。

 

 

 





