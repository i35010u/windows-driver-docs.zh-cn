---
title: 编写和部署通用传感器驱动程序
description: 本主题提供有关如何使用用户模式驱动程序框架编写和部署通用传感器驱动程序的指南， (UMDF) 版本2。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5b69ee9b0d4db65cc31d987e34d89f1e125cee0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812091"
---
# <a name="write-and-deploy-your-universal-sensor-driver"></a>编写和部署通用传感器驱动程序


本主题提供有关如何使用用户模式驱动程序框架编写和部署通用传感器驱动程序的指南， (UMDF) 版本2。

## <a name="write-a-generic-umdf-20-driver"></a>写入一般 UMDF 2.0 驱动程序


若要构建通用的 UMDF 2.0 驱动程序，请参阅 [使用通用 Windows 驱动程序入门](../develop/getting-started-with-windows-drivers.md)，并按照使用用户模式驱动程序 [构建通用](../develop/building-a-windows-driver.md)WINDOWS 驱动程序 **(UMDF V2)** 模板中的步骤进行操作。

## <a name="customize-the-generic-umdf-20-driver-files"></a>自定义一般 UMDF 2.0 驱动程序文件


当你开发并构建此通用的 UMDF 2.0 驱动程序时，它将创建相当多的样板文件，其中包括：

-   标头文件，包括 *设备 .h* 和 *驱动程序 .h*
-   源文件，包括 *设备 .cpp* 和 *驱动程序 .cpp*

自定义此通用 UMDF 2.0 驱动程序时，必须记住以下目标：

-   [使驱动程序可加载](make-the-driver-loadable.md)
-   [连接到硬件](connect-to-hardware.md)
-   [从硬件读取数据](read-data-from-hardware.md)

有关代码片段，并说明如何进行这些更新，请参阅上一列表中的主题。

更新一般文件以针对传感器自定义它们后，请参阅以下主题：

-   [查看 INX 文件](review-and-revise-the-inf-file.md)
-   [构建传感器驱动程序](build-the-sensor-driver.md)
-   [安装传感器驱动程序](install-the-sensor-driver.md)

