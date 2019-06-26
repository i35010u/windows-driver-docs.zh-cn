---
title: 编写设备安装应用程序
description: 编写设备安装应用程序
ms.assetid: 9927e2e0-6c8e-437f-98ce-595bd304ec72
keywords:
- 安装应用程序 WDK，关于编写安装应用程序
- 设备安装应用程序 WDK，如何编写安装应用程序
- 设备安装程序 WDK 设备安装，编写安装应用程序
- 安装设备 WDK，编写安装应用程序
- 编写设备安装应用程序
- 安装应用程序 WDK
- 设备安装应用程序 WDK
- 应用程序 WDK 设备安装
- 设备安装 WDK，应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e7bff2a6d3601234d40d5a5f931e4a88c7b999e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363495"
---
# <a name="writing-a-device-installation-application"></a>编写设备安装应用程序





**请注意**  通用或移动设备的驱动程序包中不支持在本部分中所述的功能。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

如果您的驱动程序打包安装这些组件。 设备安装应用程序和分发媒体应符合自动运行，以便自动运行该应用程序时自动启动用户插入分发介质。 有关自动运行的详细信息，请参阅[创建 AutoRun-Enabled 应用程序](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/cc144206(v=vs.85))。

有关如何编写设备安装应用程序的指南，请参阅[编写设备安装应用程序的指导原则](guidelines-for-writing-device-installation-applications.md)。

你[驱动程序包](driver-packages.md)必须处理两种情况下：

1.  用户插入分发介质之前，插入在您的硬件。 这通常称为[硬件第一个安装](hardware-first-installation.md)。

2.  用户在您的硬件插入前插入分发介质。 这通常称为[软件的第一个安装](software-first-installation.md)。

 

 





