---
title: 枚举子设备的显示适配器
description: 枚举子设备的显示适配器
ms.assetid: 3bec2117-aef4-41fc-b88a-0081c7c9fe3d
keywords:
- 视频存在网络 WDK 显示，显示适配器子设备
- VidPN WDK 显示，显示适配器子设备
- 子设备 WDK 视频存在网络
- 显示适配器子设备 WDK 视频存在网络
- 枚举子设备 WDK 视频存在网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 829713c12927b7a9d544f107f8902d78a42c1868
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519275"
---
# <a name="enumerating-child-devices-of-a-display-adapter"></a>枚举子设备的显示适配器


以下系列步骤描述了显示端口驱动程序、 显示微型端口驱动程序和视频存在的网络 (VidPN) 管理器在初始化时，若要枚举的显示适配器的子设备的协作方式。

1.  显示端口驱动程序调用显示微型端口驱动程序[ **DxgkDdiStartDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560775)函数。 *DxgkDdiStartDevice*返回 (在*NumberOfChildren*参数) 的设备 （或可能会变得通过停靠） 数显示适配器的子级。 *DxgkDdiStartDevice*也会返回 (在*NumberOfVideoPresentSources*参数) 支持的显示适配器的视频存在源 N 数。 随后将由数字 0，1，标识这些视频显示源...N -1.

2.  显示端口驱动程序调用显示微型端口驱动程序[ **DxgkDdiQueryChildRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff559750)函数，该枚举子设备显示适配器的函数。 *DxgkDdiQueryChildRelations*的数组中填充[ **DXGK\_子\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff561001)结构： 一个用于每个子设备。 请注意，载入的显示适配器的所有子设备： 监视器和其他外部连接到设备的显示适配器不考虑子设备。 有关详细信息，请参阅[子设备的显示适配器](child-devices-of-the-display-adapter.md)。 *DxgkDdiQueryChildRelations*必须枚举可能的子设备，以及在初始化时实际存在的子设备。 例如，如果便携式计算机连接到停靠工作站将导致新的视频输出的外观*DxgkDdiQueryChildRelations*必须枚举而不考虑是否视频输出的计算机停靠在初始化时。 此外，如果连接到的视频输出连接器的硬件保护装置将允许多台监视器中共享连接器， *DxgkDdiQueryChildRelations*必须枚举硬件保护装置，不管是硬件保护装置的每个分支的子设备在初始化时连接。

3.  每个子设备 （枚举步骤 1 中所述） HPD 感知值**HpdAwarenessInterruptible**或**HpdAwarenessPolled**，显示端口驱动程序调用显示微型端口驱动程序的[ **DxgkDdiQueryChildStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff559754)函数来确定子设备是否具有连接到它的外部设备。

4.  显示端口驱动程序将创建为满足以下条件之一，每个子设备 PDO:
    -   子设备具有 HPD 感知值**HpdAwarenessAlwaysConnected**。
    -   子设备具有 HPD 感知值**HpdAwarenessPolled**或**HpdAwarenessInterruptible**，和操作系统能识别从前面的查询或子设备的通知外部设备连接。

5.  显示端口驱动程序调用显示微型端口驱动程序[ **DxgkDdiQueryDeviceDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff559761)函数为每个子设备满足以下条件之一：

    -   已知子设备具有连接的外部设备。
    -   假定子设备已连接的外部设备。
    -   子设备都有一种**TypeOther**。

    *DxgkDdiQueryDeviceDescriptor*返回扩展的显示信息的数据 (EDID) 块，如果已连接的监视器 （或其他显示设备） 支持 EDID 描述符。

    注意：在初始化期间，显示端口驱动程序调用*DxgkDdiQueryDeviceDescriptor*为每个监视器，以便获取监视器的 EDID 的第一个 128 字节块。 它在初始化时需要提供显示端口驱动程序：即插即用硬件 ID、 实例 ID、 兼容 Id 和设备的文本。 在更高版本时，监视器类功能驱动程序 (Monitor.sys) 调用*DxgkDdiQueryDeviceDescriptor*为每个监视器，若要获取的第一个 128 字节 EDID 块和额外的 128 个字节 EDID 扩展块。 这意味着显示微型端口驱动程序将被调用两次以提供每个监视器 EDID 的第一个 128 字节块。

6.  VidPN 管理器获取标识符的所有视频显示源和视频显示适配器支持的显示目标。 视频显示源由数字 0，1，标识...N-1，其中 N 是显示微型端口驱动程序返回的源的数量*DxgkDdiStartDevice*函数。 视频显示目标具有微型端口驱动程序在以前创建的唯一整数标识符*DxgkDdiQueryChildRelations*。 类型的每个子设备**TypeVideoOutput**与视频显示目标，并**ChildUid**成员的子设备 DXGK\_子\_描述符结构用作标识符的视频显示目标。

7.  VidPN manager 使用以下过程来生成初始 VidPN。
    -   如果最后一个已知的良好 VidPN 记录在注册表中，使用它作为初始 VidPN。

    -   否则，调用显示微型端口驱动程序[ **DxgkDdiRecommendFunctionalVidPn** ](https://msdn.microsoft.com/library/windows/hardware/ff559775)函数来获取初始 VidPN。

    -   如果*DxgkDdiRecommendFunctionalVidPn*失败，返回的功能 VidPN 可接受，创建简单 VidPN，它包含一个视频存在路径; 也就是说，一个 （源、 目标） 对。 调用显示微型端口驱动程序[ **DxgkDdiIsSupportedVidPn** ](https://msdn.microsoft.com/library/windows/hardware/ff559684)函数来验证，建议的 VidPN 将正常工作。 如果*DxgkDdiIsSupportedVidPn*报表建议的 VidPN 将无法工作，不断尝试，直到找到适合 VidPN。

    -   调用显示微型端口驱动程序[ **DxgkDdiEnumVidPnCofuncModality** ](https://msdn.microsoft.com/library/windows/hardware/ff559649)函数来确定可用于 VidPN 的源和目标模式。

 

 





