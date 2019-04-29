---
title: 将 Windows NT 4.0 微型端口驱动程序转换为 Windows 2000 版本
description: 将 Windows NT 4.0 微型端口驱动程序转换为 Windows 2000 版本
ms.assetid: a55192c6-3de4-4433-8825-3393f2bce04a
keywords:
- 微型端口驱动程序 WDK Windows 2000 多个 Windows 版本中，将转换的 Windows NT 4.0 驱动程序
- 转换微型端口驱动程序 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76a5f6f5630961afe00a0c31195eb865cfb3abcb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384510"
---
# <a name="converting-a-windows-nt-40-miniport-driver-to-windows-2000"></a>将 Windows NT 4.0 微型端口驱动程序转换为 Windows 2000 版本


## <span id="ddk_converting_a_windows_nt_4_0_miniport_driver_to_windows_2000_gg"></span><span id="DDK_CONVERTING_A_WINDOWS_NT_4_0_MINIPORT_DRIVER_TO_WINDOWS_2000_GG"></span>


Windows 2000 和更高版本的微型端口驱动程序，可以轻松地成为很好的 Windows NT 4.0 和以前的微型端口驱动程序。 以下是一些提供插支持，需要在 Windows 2000 和更高版本的微型端口驱动程序所需的更新：

-   请参阅[插和视频微型端口驱动程序 （Windows 2000 模式） 中的电源管理](plug-and-play-and-power-management-in-video-miniport-drivers--windows-.md)为必须实现的新函数的列表。 请务必初始化的新成员[**视频\_HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff570505)以指向这些新函数。

-   更新对调用[ **VideoPortInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff570320)在你[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff556159)函数。 第四个参数 (*HwContext*) 必须**NULL** Windows 2000 及更高版本。

-   更新你[ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)函数。 适用于设备上的可枚举的总线*HwVidFindAdapter*必须按如下所示更改：

    -   删除你的大部分设备检测代码。 这是因为调用[ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332) Windows 2000 上意味着，即插即用 manager 已检测到设备。
    -   调用[ **VideoPortGetAccessRanges** ](https://msdn.microsoft.com/library/windows/hardware/ff570302)以获取该设备将响应的总线相对物理地址。 PnP 管理器分配这些地址。
    -   如果该驱动程序支持多个设备类型，确定设备的类型。
    -   忽略[ *Again* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)参数。 这是因为系统将调用*HwVidFindAdapter*仅一次，每个设备。

    对于如 ISA nonenumerable 总线上的设备，即插即用仍会尝试启动设备，尽管它负责[ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)来确定设备是否实际存在。

-   更新 **。制造业**部分中的驱动程序的 INF 文件以包括设备和供应商 id。 这是必需的以便 PnP 管理器可以将设备与其 INF 文件关联。 2000 及更高版本的的 Windows NT 4.0 的和已更新 Windows 示例 **。制造业**部分按照：

    ```cpp
    [ABC.Mfg]   ; Windows NT V4.0 INF
    %ABC% ABC Graphics Accelerator A = abc
    %ABC% ABC Graphics Accelerator B = abc

    [ABC.Mfg]   ; Windows 2000 and later INF
    %ABC% ABC Graphics Accelerator A = abc, PCI\VEN_ABCD&DEV_0123
    %ABC% ABC Graphics Accelerator B = abc, PCI\VEN_ABCD&DEV_4567
    ```

可以使用*geninf.exe*工具，它包含与驱动程序开发工具包 (DDK) 来生成 INF。 (在 DDK 前面带有 Windows Driver Kit \[WDK\]。)请记住，但是，该*geninf.exe*不会创建 INF Windows NT 4.0 的。 必须修改生成的 INF 文件*geninf.exe*如果你想要支持 Windows NT 4.0。 请参阅[创建图形 INF 文件](creating-graphics-inf-files.md)的更多详细信息。

Windows 2000 和更高版本的视频端口作为旧驱动程序支持 Windows NT 4.0 微型端口驱动程序。 无法从系统中删除旧的微型端口驱动程序的图形适配器，而系统正在运行，也不会自动添加到正在运行的系统时检测到旧的微型端口驱动程序。

 

 





