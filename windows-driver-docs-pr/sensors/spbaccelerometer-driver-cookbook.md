---
title: SpbAccelerometer 驱动程序指南
description: SpbAccelerometer 驱动程序指南
ms.assetid: 3E7875E1-0810-4698-A5E1-7A4C6C366967
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acfe2ad3fbaf7a32d05485e33b6a05b0a419a8bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519247"
---
# <a name="spbaccelerometer-driver-cookbook"></a>SpbAccelerometer 驱动程序指南


## <a name="get-started"></a>立即开始行动


本指南演示如何开始使用适用于 Windows 8.1 和早期操作系统 （SpbAccelerometer 示例驱动程序） 开发的示例驱动程序。

>[!NOTE]
> 若要评估 Windows 10 和更高版本操作系统的传感器驱动程序示例，请参阅[传感器示例驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/sensors)。 有关如何开发和生成传感器驱动程序适用于 Windows 10 和更高版本操作系统的信息，请参阅[编写和部署通用传感器驱动程序](write-and-deploy-your-universal-sensor-driver.md)。

 

首先，将通过在 Shark Cove 板上安装 Windows。 它们将配置加速感应器，并将其附加到 Shark Cove 板。 接下来，你将安装 Microsoft Visual Studio Express 和 Windows Driver Kit (WDK)。 然后，你将安装的示例驱动程序。 完成这些任务后，可以开始探索的示例驱动程序。

有关 Shark Cove 板的信息，请参阅[SharksCove.org](https://go.microsoft.com/fwlink/p/?linkid=403167)。

### <a name="required-hardware"></a>所需的硬件

在开始之前，请确保具备以下硬件：

-   附带电源线和适配器的 Sharks Cove 板。
-   [ADXL345](https://go.microsoft.com/fwlink/p/?linkid=401463)加速感应器/专题板
-   USB 集线器
-   USB 键盘
-   USB 鼠标
-   USB 网络适配器
-   监视器和 HDMI 电缆（可能还需适配器）

### <a name="document-conventions"></a>文档约定

在部分中描述的示例驱动程序，会在每个部分标题后看到短表：

![文档约定](images/document-conventions.png)

这些表确定的源代码模块和在该节中讨论的类。 使用此信息来打开模块，并在 Visual Studio 中查看其相应的代码。

 

 




