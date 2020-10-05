---
title: 通过共同安装程序启动设备安装应用程序
description: 通过辅助安装程序启动设备安装应用程序的指南
ms.assetid: 94b21eef-5660-4d05-8eb5-da6589c85e65
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 112e42811b804b020a788c40aba9abc0f5e749c4
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733297"
---
# <a name="guidelines-for-starting-device-installation-applications-through-co-installers"></a>通过辅助安装程序启动设备安装应用程序的指南


对于提供完成安装操作的共同安装程序，必须遵循以下准则：

-   在设备安装应用程序完成之前，共同安装程序不得退出其 "完成安装" 页或 "完成-安装" 操作。 如果共同安装程序早退出，而另一个驱动程序需要重新启动，则 Windows 可能会在应用程序完成之前重新启动计算机。

-   共同安装程序应首先在分发介质上查找设备安装应用程序，如果该应用程序存在，则会以静默方式开始安装过程。

    如果分发介质不存在，则共同安装程序应为用户提供从 Internet 插入或下载设备安装应用程序的选择。 如果用户选择插入介质，则共同安装程序应检测新的媒体通知，以无提示方式退出，并允许介质的自动运行过程启动设备安装应用程序。

    共同安装程序可通过侦听 WM_DEVICECHANGED/DBT_DEVICEARRIVAL 消息来检测新媒体，dbch_devicetype 设置为 DBT_DEVTYP_VOLUME，dbcv_flags 设置为 DBTF_MEDIA。

    有关详细信息，请参阅 [检测媒体插入或删除](/windows/win32/devio/detecting-media-insertion-or-removal)。

-   共同安装程序永远不应假定分发媒体在安装过程中可用。 例如，共同安装程序绝不应使用 %1% DirId 从共同安装程序中查找媒体。

    在 Windows Vista 和更高版本的 Windows 中，将在复制到驱动程序存储区后调用共同安装程序。 此时，可能会删除分发媒体，这就是避免提示用户使用媒体的原因。 例如，假设用户执行 [软件第一次安装](software-first-installation.md)，删除分发介质，然后插入设备。 仅当用户第一次插入设备时，才会调用共同安装程序。

-   如果联合安装程序启动 Windows Internet Explorer 以下载设备安装应用程序，则它必须在保护模式下启动该应用程序，这种功能可保护用户不受恶意代码的攻击。

    有关在保护模式下启动 Internet Explorer 的详细信息，请参阅 [了解和使用受保护模式的 Internet explorer](/previous-versions/windows/internet-explorer/ie-developer/)。

有关共同安装程序的详细信息，请参阅 [编写共同安装程序](writing-a-co-installer.md)。

 

