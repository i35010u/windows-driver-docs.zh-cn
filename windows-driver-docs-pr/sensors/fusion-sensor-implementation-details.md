---
title: 合成传感器实现详细信息
description: 本部分提供有关 Windows 合成传感器驱动程序堆栈的实现详细信息。
ms.assetid: B53D76AC-127C-4B5A-B908-A647D2B3F164
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6d4cb172bf7ab859f69c9f752f655a7d2ec1617f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568924"
---
# <a name="fusion-sensor-implementation-details"></a>合成传感器实现详细信息


本部分提供有关 Windows 合成传感器驱动程序堆栈的实现详细信息。

>[!NOTE]
>Microsoft 提供了在某些平台上的合成驱动程序二进制文件和合作伙伴不能取代这些。

 

下图显示了传感器合成软件堆栈。

![合成传感器堆栈图示](images/fusion-sensor-stack.png)

合成软件堆栈由以下组件构成：

-   **传感器的本机 Api**调用的应用程序访问熔和指南针特性和功能。 Api 是 ReadFile 和 DeviceIoControl 的包装器。 这些 Api 将发送到传感器类扩展，然后处理并完成请求。

-   **传感器类扩展**为任何所需的特定于传感器的扩展性提供支持。

-   **合成驱动程序**是驱动程序的特定功能的软件部分。 它读取物理传感器，并处理数据。 此组件中实现基本指南针和熔传感器的算法。

## <a name="coordinate-systems"></a>坐标系统


下图中显示的坐标系用于所有物理传感器和融合数据。

![图示陀螺仪设备方向](images/gyroscope-orientation.png)

下图中显示的坐标系是合成算法和 Api 由用于接地/参考框架中的所有向量的约定。

![一个显示地球坐标系统 fusion 算法所用的图表](images/earth-coordinatesystem.png)

<!--
//commenting out for now, all these links are bad.
## Data structures


The following structures and enumerations are used by the fusion data part of the logical sensor driver:

-   [**VEC3D**](https://msdn.microsoft.com/library/windows/hardware/dn946712)

-   [**COORDINATE\_AXIS**](https://msdn.microsoft.com/library/windows/hardware/dn957021)

-   [**QUATERNION**](https://msdn.microsoft.com/library/windows/hardware/dn957081)

-   [**MATRIX3X3**](https://msdn.microsoft.com/library/windows/hardware/dn957074)

-   [Fusion sensor enumerations](https://go.microsoft.com/fwlink/p/?linkid=839352) and [Fusion sensor structures](https://go.microsoft.com/fwlink/p/?linkid=839355) provide information about the entire sensor fusion data structure, which include the attitude (in multiple formats) and the linear acceleration, and the compass data.
-->
 

 




