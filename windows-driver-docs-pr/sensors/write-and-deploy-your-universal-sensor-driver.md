---
title: 编写和部署通用传感器驱动程序
description: 本主题提供有关如何编写和部署通用传感器驱动程序，使用用户模式驱动程序框架 (UMDF) 版本 2 的指南。
ms.assetid: FA888CB3-5B43-47CB-907D-76C6E6B6DE5D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d675023de031890dc24c4c638e0a0a344ed852a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544924"
---
# <a name="write-and-deploy-your-universal-sensor-driver"></a>编写和部署通用传感器驱动程序


本主题提供有关如何编写和部署通用传感器驱动程序，使用用户模式驱动程序框架 (UMDF) 版本 2 的指南。

## <a name="write-a-generic-umdf-20-driver"></a>编写泛型 UMDF 2.0 驱动程序


若要生成的通用 UMDF 2.0 驱动程序，请参阅[通用 Windows 驱动程序入门](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)，并按照一节中的步骤[构建通用 Windows 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-universal-driver)，以生成通用 Windows驱动程序使用**用户模式驱动程序 (UMDF V2)** 模板。

## <a name="customize-the-generic-umdf-20-driver-fies"></a>自定义一般的 UMDF 2.0 驱动程序文件


当在开发和生成此通用 UMDF 2.0 驱动程序时，它将创建很多样板文件，其中包括：

-   标头文件，包括*Device.h*和*Driver.h*
-   源文件，其中包括*Device.cpp*和*Driver.cpp*

自定义此通用 UMDF 2.0 驱动程序时，这些是您必须牢记于心的目标：

-   [使驱动程序可加载](make-the-driver-loadable.md)
-   [连接到硬件](connect-to-hardware.md)
-   [从硬件中读取数据](read-data-from-hardware.md)

有关代码段，使用有关如何进行这些更新的说明，请参阅前面的列表中的主题。

在更新后的通用文件以自定义它们的传感器，请参阅以下主题：

-   [查看 INX 文件](review-and-revise-the-inf-file.md)
-   [生成传感器驱动程序](build-the-sensor-driver.md)
-   [安装传感器驱动程序](install-the-sensor-driver.md)

 

 




