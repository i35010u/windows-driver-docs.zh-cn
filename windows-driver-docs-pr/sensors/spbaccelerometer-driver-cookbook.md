---
title: SpbAccelerometer 驱动程序指南
description: SpbAccelerometer 驱动程序指南
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07d3c6b901da09aca40d90a15a0d0c915723a0f4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812161"
---
# <a name="spbaccelerometer-driver-cookbook"></a>SpbAccelerometer 驱动程序指南


## <a name="get-started"></a>入门


本指南演示如何开始使用为 (示例驱动程序) Windows 8.1 和早期版本的操作系统开发的示例驱动程序。

>[!NOTE]
> 若要评估适用于 Windows 10 及更高版本操作系统的传感器驱动程序示例，请参阅 [传感器示例驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/sensors)。 有关如何开发和生成适用于 Windows 10 及更高版本操作系统的传感器驱动程序的信息，请参阅 [编写和部署通用传感器驱动程序](write-and-deploy-your-universal-sensor-driver.md)。

 

首先，将 Windows 安装在带 Cove 板上。 你将配置加速感应，并将其附加到带 Cove 板。 接下来，你将 Microsoft Visual Studio Express 和 Windows 驱动程序工具包 (WDK) 安装。 然后，将安装示例驱动程序。 完成这些任务后，便可以开始探索示例驱动程序了。

### <a name="required-hardware"></a>所需硬件

在开始之前，请确保你具有以下硬件：

-   附带电源线和适配器的 Sharks Cove 板。
-   [ADXL345](https://go.microsoft.com/fwlink/p/?linkid=401463) 加速度/专题讨论板
-   USB 集线器
-   USB 键盘
-   USB 鼠标
-   USB 网络适配器
-   监视器和 HDMI 电缆（可能还需适配器）

### <a name="document-conventions"></a>文档约定

在介绍示例驱动程序的部分中，你将看到每个节标题后面的简短表格：

![文档约定](images/document-conventions.png)

这些表标识了在该部分中讨论的源模块和类。 使用此信息打开该模块，并在 Visual Studio 中查看其相应的代码。

 

 




