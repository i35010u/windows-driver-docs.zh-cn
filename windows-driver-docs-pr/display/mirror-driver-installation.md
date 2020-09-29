---
title: 镜像驱动程序安装
description: 镜像驱动程序安装
ms.assetid: 13b0ce22-f833-482c-815b-a596098ee6bc
keywords:
- 显示驱动程序 WDK Windows 2000，镜像驱动程序
- 镜像驱动程序 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbb34407f79c41bf2aa7688366b7a620379e45b5
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423691"
---
# <a name="mirror-driver-installation"></a>镜像驱动程序安装

> [!NOTE]
>
> 从 Windows 8 开始，镜像驱动程序将不会安装在系统上。 有关详细信息，请参阅 [镜像驱动程序](mirror-drivers.md)。

系统安装镜像驱动程序来响应 Win32 **ChangeDisplaySettings** 或 **ChangeDisplaySettingsEx** 调用。 你应该实现一个用户模式服务来进行这些调用，以安装镜像驱动程序并维护其设置。 使用此应用程序可以：

-   确保在启动时正确加载镜像驱动程序。 应用程序应指定 CD \_ UPDATEREGISTRY 标志来将设置保存到注册表，以便在后续启动时自动加载该驱动程序，如下所述的 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devicemodew) 信息相同。

-   通过 WM DISPLAYCHANGE 消息获取显示更改通知，对桌面更改做出适当的响应 \_ 。

示例 *Mirror.exe*（可从随 Windows 驱动程序工具包一起提供的源代码文件生成 (WDK) ）实现了用户模式服务为加载镜像驱动程序而应提供的部分操作。

安装镜像驱动程序之前，用户模式应用程序应填写指定以下显示属性的 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devicemodew) 结构：

-    (**dmPosition** 的位置) 

-   大小 (**dmPelsWidth** 和 **dmPelsHeight**) 

-   镜像显示的格式 (**dmBitsPerPel**) 

用户模式应用程序还必须通过为每个要更改的结构成员包含标志，来正确设置 **dmFields** 。 必须在桌面坐标中指定镜像显示的位置坐标;因此，它们可以跨多个设备。 若要直接镜像主显示器，镜像驱动程序应指定其位置，使其与主显示器的桌面坐标一致。

设置 DEVMODEW 结构成员后，通过在对 Win32 **ChangeDisplaySettingsEx** 函数的调用中传递此结构来更改镜像的显示设置。

镜像驱动程序安装完成后，对于与驱动程序的显示区域相交的所有呈现操作，它将被 GDI 调用。 如果镜像驱动程序只与多监视器系统中的主显示器重叠，则 GDI 可能不会将所有绘图操作发送到镜像驱动程序。

有关 **ChangeDisplaySettings** 和 **ChangeDisplaySettingsEx** 函数的详细信息，请参阅 Microsoft Windows SDK 文档，并显示更改桌面通知。