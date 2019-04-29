---
title: 媒体 GUID
description: 媒体 GUID
ms.assetid: 4209952c-0ba5-4359-b612-91529a0a46f1
keywords:
- 视频捕获 WDK AVStream，介质
- 捕获视频 WDK AVStream，介质
- 媒体 WDK 视频捕获
- pin 连接 WDK 视频捕获
- Guid WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48aeccc7edc9c8bf9d85d8cdaa9645fdd5b8d481
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370228"
---
# <a name="medium-guids"></a>媒体 GUID


微型驱动程序必须能够支持多个设备。 此外，因为电视/广播调谐器、 电视音频、 纵横制和视频捕获组件分为不同的内核流式处理筛选器，方法是进行正确上描述这些组件之间的拓扑的硬件连接所需设备，以及为多个设备上。 例如，两个生成，但未在运行筛选器关系图的支持 FM 收音机和电视捕获必须能够共存。 微型驱动程序使用媒体来提供这些方案。 此外，筛选器关系图构建应用程序，如*关系图编辑*，筛选器关系图构造期间使用介质，以确保一台设备的筛选器正确连接到另一台设备的筛选器。 例如，一台设备的调谐器筛选器不应连接到另一台设备的纵横制筛选器。

微型驱动程序描述与媒体[ **KSPIN\_MEDIUM** ](https://msdn.microsoft.com/library/windows/hardware/ff563538) GUID 数据类型成员组成的结构 (**设置**) 两个 ULONG 成员 （后跟**Id**并**标志**):

-   **设置**成员应分配表示拓扑的硬件连接的 GUID。

-   微型驱动程序必须设置**Id**设备实例的唯一值的成员。

-   **标志**成员保留供系统使用，应设置为零。

若要有多个设备出现在系统中，确保正确构造筛选器关系图**设置**KSPIN 成员\_中等结构保持不变的每个设备实例。 但是，微型驱动程序必须将分配到唯一的值**Id** KSPIN 成员\_中等结构每个设备实例。 设置失败**Id**为唯一值的成员会导致问题，在系统中存在多个设备时。 如果两个设备安装在系统中，则必须设置微型驱动程序**Id**成员添加到的每个设备实例的值。 请注意， **Id**驻留在相同的硬件，如调谐器和纵横制，片段的设备的筛选器的成员必须相同。 一种方法，以确保**Id**设备实例之间不同，成员是已微型驱动程序中创建一个全局计数器并将设备插开始时间之前设置期间递增该计数器**Id**为其值。

具体取决于内核流式处理接口的微型驱动程序遵循 （AVStream 或 Stream 类），微型驱动程序必须指定的值**Id**成员以不同的方式：

-   Stream 类微型驱动程序指定的值时处理[ **SRB\_获取\_流\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff568173)。

-   AVStream 微型驱动程序中指定值[ **KSPIN\_描述符\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)结构。 有两个不同的方式有关 AVStream 微型驱动程序指定的值在 KSPIN\_描述符\_EX 结构：

    1.  静态描述符提供全局**Id**计数器，并调用[  **\_KsEdit** ](https://msdn.microsoft.com/library/windows/hardware/ff568796)期间*添加*或*启动*调度处理程序来更改**Id**为唯一值的成员。
    2.  调用[ **KsCreateFilterFactory** ](https://msdn.microsoft.com/library/windows/hardware/ff561650)来动态创建期间的筛选器/pin 描述符*添加*或者*启动*调度处理程序。

微型驱动程序还必须调用自行注册到 Microsoft DirectShow 以允许应用程序自动构造具有电视/广播调谐器、 电视音频和纵横制筛选器的筛选器关系图，因为它们实际上不会创建一个特殊函数内核流式处理其输入和输出的 pin。 当微型驱动程序注册这些筛选器时，它应设置**Id** KSPIN 成员\_中等结构的唯一值。 如果未设置微型驱动程序不会**Id** KSPIN 成员\_中等结构为唯一值，然后自动关系图构建应用程序可能无法加载必需的相邻筛选器。 但是，手动筛选器的关系图构建，在编辑关系图，可能仍正常工作。

若要使用 DirectShow 注册微型驱动程序：

-   Stream 类微型驱动程序调用[ **StreamClassRegisterFilterWithNoKSPins** ](https://msdn.microsoft.com/library/windows/hardware/ff568261)函数来注册 DirectShow 筛选器。

-   AVStream 微型驱动程序调用[ **KsRegisterFilterWithNoKSPins** ](https://msdn.microsoft.com/library/windows/hardware/ff566773)函数来注册 DirectShow 筛选器。

-   或者，如果微型驱动程序遵循 BDA 模型和特定的多个实例[ **KSFILTER\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff562553)在某些特定的结构[ **KSDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff561681)结构在同一个内核流式处理类别中注册，请调用[ **KsFilterFactoryUpdateCacheData** ](https://msdn.microsoft.com/library/windows/hardware/ff562540) (或[**BdaFilterFactoryUpdateCacheData**](https://msdn.microsoft.com/library/windows/hardware/ff556455)) 函数来注册 DirectShow 筛选器。

KSPIN\_中等结构返回从任一 SRB\_获取\_流\_信息 （适用于 Stream 类微型驱动程序） 或 KSPIN\_描述符\_EX （适用于 AVStream 微型驱动程序） 必须匹配KSPIN\_中等成员返回中的以下属性：

-   **中等**的成员[ **KSPROPERTY\_纵横制\_PININFO\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565123)结构[ **KSPROPERTY\_纵横制\_PININFO**](https://msdn.microsoft.com/library/windows/hardware/ff565121)。 如果介质不匹配，则关系图构建微型驱动程序的筛选器和关系图中的相邻筛选器之间可能会失败。

-   **VideoMedium**并**AudioMedium**的成员[ **KSPROPERTY\_调谐器\_CAPS\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565828)的结构[ **KSPROPERTY\_调谐器\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/ff565825)。

-   **InputMedium**并**OutputMedium**的成员[ **KSPROPERTY\_TVAUDIO\_CAPS\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565936)的结构[ **KSPROPERTY\_TVAUDIO\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/ff565933)。

除了正确实现媒体和中等 Guid，有必要遵循其他准则，以确保进程可使用多个筛选器关系图。 微型驱动程序必须锁定之前的筛选器图形转换到的任何硬件资源**KSSTATE\_ACQUIRE** KSSTATE 的值。 这有助于确保两个生成，但未在运行筛选器关系图而不会干扰另一个可以共存。

有关介质，包括如何实现它们，请参阅[AVStream 模拟硬件示例驱动程序 (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)。

**请注意**  :当 Windows 驱动程序工具包中的示例代码中派生新的微型驱动程序，必须生成介质，用来反映设备的唯一的硬件拓扑结构的新 GUID 值。 如果不这样做可能会导致另一台设备为定义介质与其碰撞的一台设备的介质。

 

 

 




