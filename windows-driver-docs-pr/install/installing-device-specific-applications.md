---
title: 安装特定于设备的应用程序
description: 安装特定于设备的应用程序
keywords:
- 安装应用程序 WDK，特定于设备的应用程序
- 设备安装应用程序 WDK，特定于设备的应用程序
- 设备特定的应用程序 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8c8f017a196e98d62e22849d9ee2b68097acd63
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794867"
---
# <a name="installing-device-specific-applications"></a>安装特定于设备的应用程序





如果你的分发介质包含设备特定的应用程序，你可以使用以下方法来安装这些应用程序：

-   使用设备共同安装程序通过使用 " [完成-安装" 操作](finish-install-actions--windows-vista-and-later-.md)来安装应用程序。

    如果用户在插入分发媒体之前插入设备，则这称为 [硬件第一次安装](hardware-first-installation.md)。 如果收件箱驱动程序不支持该设备，Windows 将调用安装过程中介质提供的共同安装程序。

    共同安装程序应确定是否已安装了特定于设备的应用程序。 如果没有，则共同安装程序应执行以下操作之一

    1.  在分发介质上启动 *设备安装应用程序* 以安装特定于设备的应用程序。
    2.  提示用户从 Internet 下载设备安装应用程序的较新版本。

    独立硬件供应商 (Ihv) 可以使用各种方法来提供 [硬件优先安装](hardware-first-installation.md) 解决方案，以便安装特定于设备的应用程序。 有关这些方法的详细信息，请参阅 [Device-Specific 应用程序的硬件首次安装](device-installation-application-not-included-in-the-driver-package.md)。

    有关共同安装程序的详细信息，请参阅 [编写共同安装程序](writing-a-co-installer.md)。

-   使用 Windows Installer 安装特定于设备的应用程序的设备安装应用程序。

    如果用户在插入设备前插入分布介质，则这称为 [软件优先安装](software-first-installation.md)。 介质的自动运行调用设备安装应用程序应该确定是否已安装了设备特定的应用程序，如果没有，则应使用 Windows Installer 安装它们。 有关详细信息，请参阅 Windows SDK 文档。

 

 





