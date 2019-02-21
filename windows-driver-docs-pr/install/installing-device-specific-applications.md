---
title: 安装特定于设备的应用程序
description: 安装特定于设备的应用程序
ms.assetid: 47e54ea6-f391-420a-aa69-caf7225b1147
keywords:
- 安装应用程序 WDK，特定于设备的应用程序
- 设备安装应用程序 WDK，特定于设备的应用程序
- 特定于设备的应用程序 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 095f4ec16702756e9126a076a3f5e0b5f06f0770
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519093"
---
# <a name="installing-device-specific-applications"></a>安装特定于设备的应用程序





如果分发介质中包含特定于设备的应用程序，您可以使用以下方法安装这些应用程序：

-   使用设备共同安装程序安装的应用程序通过使用[完成安装操作](finish-install-actions--windows-vista-and-later-.md)。

    如果用户插入设备插入分发介质之前，这称为[硬件第一个安装](hardware-first-installation.md)。 如果收件箱驱动程序不支持该设备，Windows 会调用共同安装程序在安装过程中提供的介质。

    辅助安装程序应确定是否已安装了特定于设备的应用程序。 如果它们尚未打开，辅助安装程序应执行以下项之一

    1.  启动*设备安装应用程序*分发介质安装特定于设备的应用程序上。
    2.  提示用户从 Internet 下载的设备安装应用程序的较新版本。

    独立硬件供应商 (Ihv) 可以使用各种方法来提供[硬件第一个安装](hardware-first-installation.md)用于安装特定于设备的应用程序的解决方案。 有关这些方法的详细信息，请参阅[硬件第一个安装的特定于设备的应用程序](hardware-first-installation-of-device-specific-applications.md)。

    有关共同安装程序的详细信息，请参阅[编写共同安装程序](writing-a-co-installer.md)。

-   使用设备安装应用程序使用 Windows 安装程序来安装特定于设备的应用程序。

    如果用户插入设备之前插入分发介质，因此将此称为[软件的第一个安装](software-first-installation.md)。 中的自动运行调用设备安装应用程序应确定是否已安装特定于设备的应用程序，如果它们尚未打开，它应使用 Windows 安装程序安装它们。 有关详细信息，请参阅 Windows SDK 文档。

 

 





