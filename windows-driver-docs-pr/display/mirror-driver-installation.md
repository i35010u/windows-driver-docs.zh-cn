---
title: 镜像驱动程序安装
description: 镜像驱动程序安装
ms.assetid: 13b0ce22-f833-482c-815b-a596098ee6bc
keywords:
- 显示驱动程序 WDK Windows 2000 中，镜像驱动程序
- 镜像驱动程序 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed4b2b1df3a82f7bf2f5bab0061159ca5d32f0a0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385594"
---
# <a name="mirror-driver-installation"></a>镜像驱动程序安装


## <span id="ddk_mirror_driver_installation_gg"></span><span id="DDK_MIRROR_DRIVER_INSTALLATION_GG"></span>


系统将镜像驱动程序安装以响应 Win32 **ChangeDisplaySettings**或**ChangeDisplaySettingsEx**调用。 应实现用户模式服务以使这些调用安装镜像驱动程序和维护其设置之一。 使用此应用程序：

-   请确保在启动时正确加载镜像驱动程序。 应用程序应指定在 CDS\_UPDATEREGISTRY 标志，用于将设置保存到注册表，以便自动将上具有相同的后续启动时加载驱动程序[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)如下所述的信息。

-   适当地为响应通过获取显示的桌面更改更改通知通过 WM\_DISPLAYCHANGE 消息。

该示例*Mirror.exe*、 发售的 Windows Driver Kit (WDK) 使用了哪些可以生成的源代码文件，操作用户模式服务的子集加载镜像驱动程序而应提供实现。

用户模式应用程序安装镜像驱动程序之前，应填写[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)结构，它指定显示以下属性：

-   位置 (**dmPosition**)

-   大小 (**dmPelsWidth**并**dmPelsHeight**)

-   镜像显示的格式 (**dmBitsPerPel**)

用户模式应用程序还必须设置**dmFields**相应地，通过包括的每个要更改这些结构成员的标志。 以桌面坐标; 必须指定镜像的显示位置坐标在这种情况下，它们可以跨多个设备。 若要直接镜像主显示器，请镜像驱动程序应指定其位置主显示器的桌面坐标停机的时间。

设置了 DEVMODEW 结构成员后，通过将此结构传递到 Win32 调用中更改镜像的显示设置**ChangeDisplaySettingsEx**函数。

镜像驱动程序安装后，它将由调用 GDI 相交驱动程序的显示区域的所有呈现操作。 如果镜像驱动程序与多监视器系统中重叠仅主显示器，GDI 可能所有绘制操作发送到镜像驱动程序。

请参阅的详细信息的 Microsoft Windows SDK 文档**ChangeDisplaySettings**并**ChangeDisplaySettingsEx**函数，并显示更改桌面的通知。

**请注意**  从 Windows 8 开始，镜像驱动程序不会安装在系统上。 有关详细信息，请参阅[镜像驱动程序](mirror-drivers.md)。

 

 

 





