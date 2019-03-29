---
title: 开始通过共同安装程序的设备安装应用程序
description: 通过辅助安装程序启动设备安装应用程序的指南
ms.assetid: 94b21eef-5660-4d05-8eb5-da6589c85e65
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5bc455a9c54ef9811c6b35ebff8f396b12f5575
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567429"
---
# <a name="guidelines-for-starting-device-installation-applications-through-co-installers"></a>通过辅助安装程序启动设备安装应用程序的指南


为共同安装程序提供完成安装操作，必须遵循以下准则：

-   完成设备安装应用程序之前，辅助安装程序必须从其完成安装页或完成安装操作退出。 如果共同安装程序提前退出，并且另一个驱动程序需要重启，Windows 可能会重新启动计算机，该应用程序完成之前。

-   辅助安装程序应首先查找分发介质上的设备安装应用程序和，如果应用程序存在，则以无提示方式开始安装过程。

    如果分发介质不存在，辅助安装程序应提供用户插入介质或从 Internet 下载的设备安装应用程序的选择。 如果用户选择要插入的媒体，辅助安装程序应检测新的媒体通知，请以无提示方式退出，并允许启动设备安装应用程序中的自动运行进程。

    辅助安装程序可以通过使用设置为 DBT_DEVTYP_VOLUME 和 dbcv_flags 设置为 DBTF_MEDIA dbch_devicetype WM_DEVICECHANGED/DBT_DEVICEARRIVAL 消息侦听检测新的媒体。

    有关详细信息，请参阅[检测媒体插入或删除](https://go.microsoft.com/fwlink/p/?linkid=161958)。

-   辅助安装程序应永远不会假定分发介质安装过程中可用。 例如，辅助安装程序永远不应使用 %1 %dirid 若要查找在共同安装程序中的媒体。

    在 Windows Vista 和更高版本的 Windows 中，将其复制到驱动程序存储区之后，将调用共同安装程序。 此时，在分发媒体可能被删除，这就是为什么很重要，可以避免提示用户提供该介质。 例如，假设用户执行[软件的第一个安装](software-first-installation.md)分发介质中删除，然后插入设备。 仅当用户第一次插入设备中时，被调用共同安装程序。

-   如果共同安装程序将启动 Windows Internet Explorer 下载设备安装应用程序，它必须在受保护模式下，它具有保护用户免受恶意代码的功能来启动它。

    有关在受保护模式下启动 Internet Explorer 的详细信息，请参阅[了解和使用受保护模式 Internet Explorer 中](https://go.microsoft.com/fwlink/p/?linkid=133163)。

有关共同安装程序的详细信息，请参阅[编写共同安装程序](writing-a-co-installer.md)。

 

 





