---
title: 合成传感器实现细节
description: 本部分提供有关 Windows 合成传感器驱动程序堆栈的实现细节。
ms.assetid: B53D76AC-127C-4B5A-B908-A647D2B3F164
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f870c69122d8f79f637eddd4b8acc784d6b10985
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733055"
---
# <a name="fusion-sensor-implementation-details"></a>合成传感器实现细节


本部分提供有关 Windows 合成传感器驱动程序堆栈的实现细节。

>[!NOTE]
>Microsoft 在某些平台上提供了合成驱动程序二进制文件，无法将其替换为合作伙伴。

 

下图显示了传感器合成软件堆栈。

![显示合成传感器堆栈的关系图](images/fusion-sensor-stack.png)

合成软件堆栈包含以下组件：

-   应用程序调用 **传感器本机 api** 来访问合成和罗盘的特性和功能。 Api 是 ReadFile 和 DeviceIoControl 的包装器。 这些 Api 将发送到传感器类扩展，后者随后处理并完成请求。

-   **传感器类扩展**为任何所需的特定于传感器的扩展性提供支持。

-   **合成驱动程序**是驱动程序的特定于功能的软件部分。 它读取物理传感器并处理数据。 指南针和合成传感器的算法是在此组件中实现的。

## <a name="coordinate-systems"></a>坐标系统


下图中显示的坐标系统用于所有物理传感器和合成数据。

![显示陀螺仪设备方向的关系图](images/gyroscope-orientation.png)

下图中显示的坐标系统是合成算法和 Api 用于引用的地球/地面帧中的所有矢量的约定。

![显示合成算法使用的地球坐标系统的关系图](images/earth-coordinatesystem.png)

<!--
//commenting out for now, all these links are bad.
## Data structures


The following structures and enumerations are used by the fusion data part of the logical sensor driver:

-   [**VEC3D**](./index.md)

-   [**COORDINATE\_AXIS**](./index.md)

-   [**QUATERNION**](./index.md)

-   [**MATRIX3X3**](./index.md)

-   [Fusion sensor enumerations](./index.md) and [Fusion sensor structures](./index.md) provide information about the entire sensor fusion data structure, which include the attitude (in multiple formats) and the linear acceleration, and the compass data.
-->
