---
title: 设置视频适配器访问范围
description: 设置视频适配器访问范围
ms.assetid: 250c5611-c6f5-49b5-94bc-93a1b43312e6
keywords:
- 视频适配器访问范围 WDK 微型端口
- 范围 WDK 微型端口
- 逻辑范围地址 WDK 微型端口
- 适配器访问范围 WDK 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f01a2dbbd733a69ba0ac5f19d39216acece5929f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575555"
---
# <a name="setting-up-video-adapter-access-ranges"></a>设置视频适配器访问范围


## <span id="ddk_setting_up_video_adapter_access_ranges_gg"></span><span id="DDK_SETTING_UP_VIDEO_ADAPTER_ACCESS_RANGES_GG"></span>


一个数组[**视频\_访问\_范围**](https://msdn.microsoft.com/library/windows/hardware/ff570498)-类型的元素描述一个或多个范围的内存和/或视频适配器进行解码的 I/O 端口。 此数组中的每个访问范围元素包含总线相对物理地址的值。

微型端口驱动程序[ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)例程必须声明所有 PCI 内存和端口或范围的适配器将响应的端口。 具体取决于适配器并**AdapterInterfaceType**中的值[**视频\_端口\_配置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff570531)， *HwVidFindAdapter*可以调用的以下一些 **视频端口 * * * Xxx*函数，以获取必要的总线相关配置数据：

[**VideoPortGetAccessRanges**](https://msdn.microsoft.com/library/windows/hardware/ff570302)

[**VideoPortGetBusData**](https://msdn.microsoft.com/library/windows/hardware/ff570306)

[**VideoPortGetDeviceData**](https://msdn.microsoft.com/library/windows/hardware/ff570311)

[**VideoPortGetRegistryParameters**](https://msdn.microsoft.com/library/windows/hardware/ff570316)

[**VideoPortVerifyAccessRanges**](https://msdn.microsoft.com/library/windows/hardware/ff570377)

如果*HwVidFindAdapter*无法通过调用获取总线相对访问范围信息**VideoPortGetBusData**或**VideoPortGetAccessRanges**，或从与注册表**VideoPortGetDeviceData**或**VideoPortGetRegistryParameters**，微型端口驱动程序应具有访问权限范围的总线相对默认值的一组。

每个*HwVidFindAdapter*函数必须将每个已声明的总线相对物理地址范围映射到与内核模式地址空间中的范围**VideoPortGetDeviceBase**逻辑地址范围尤其是在多个总线机。

使用映射的逻辑范围地址，该驱动程序可以调用 **VideoPortRead * * * Xxx*和 **VideoPortWrite * * * Xxx*函数来读取或写入到适配器。 这些内核模式地址也可以传递给[ **VideoPortCompareMemory**](https://msdn.microsoft.com/library/windows/hardware/ff570285)， [ **VideoPortMoveMemory**](https://msdn.microsoft.com/library/windows/hardware/ff570332)， [**VideoPortZeroDeviceMemory**](https://msdn.microsoft.com/library/windows/hardware/ff570492)，和/或[ **VideoPortZeroMemory**](https://msdn.microsoft.com/library/windows/hardware/ff570493)。 对于在 I/O 空间中映射的范围，微型端口驱动程序调用 **VideoPortReadPort * * * Xxx*和 **VideoPortWritePort * * * Xxx*函数。 对于在内存中映射的范围，微型端口驱动程序调用 **VideoPortReadRegister * * * Xxx*和 **VideoPortWriteRegister * * * Xxx*函数。

[ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)函数*必须始终*调用[ **VideoPortVerifyAccessRanges** ](https://msdn.microsoft.com/library/windows/hardware/ff570377)或[ **VideoPortGetAccessRanges** ](https://msdn.microsoft.com/library/windows/hardware/ff570302)成功*之前*它将调用[ **VideoPortGetDeviceBase**](https://msdn.microsoft.com/library/windows/hardware/ff570310).

-   任何成功调用**VideoPortVerifyAccessRanges**或**VideoPortGetAccessRanges**微型端口驱动程序的特定于总线的视频内存上声明并注册地址或 I/O 端口建立其在注册表中的适配器。 很重要，但请注意，任何后续调用**VideoPortVerifyAccessRanges**或**VideoPortGetAccessRanges**将导致该驱动程序的先前声明的资源要擦除和替换为调用的函数传递到最新的范围。 因此，如果驱动程序通过单独调用这些函数的声明范围，它必须传递所有范围数组，其中包含已声明。

-   *HwVidFindAdapter*可以声明一小组的适配器的访问范围，使用此组来确定适配器是否是一个微型端口驱动程序支持，并声明一套完整的访问范围的受支持的适配器通过再次调用**VideoPortGetAccessRanges**或**VideoPortVerifyAccessRanges**。 同样，对这些每次成功调用**视频端口...AccessRanges**特定适配器的例程将覆盖注册表中的调用方的上一个声明。

-   若要声明其他类型的硬件资源，例如中断矢量，微型端口驱动程序应设置适当的值在视频\_端口\_CONFIG\_信息并调用**VideoPortVerifyAccessRanges**，或应调用**VideoPortGetAccessRanges**。

-   调用**VideoPortGetAccessRanges**或**VideoPortVerifyAccessRanges**成功可确保微型端口驱动程序不会尝试使用注册或由另一个已在使用设备的内存地址驱动程序。

-   声明在注册表中的适配器的总线相对硬件资源对于其适配器阻止加载尝试使用相同的访问权限范围 （和其他硬件资源） 的更高版本的驱动程序。 它还可以阻止随后加载驱动程序更改的视频适配器的初始化的状态。

解码的旧的资源的硬件的微型端口驱动程序必须声明中的这些资源及其**DriverEntry**例程，或如果实现，其*HwVidLegacyResources*例程。 旧资源是设备的 PCI 配置空间中未列出这些资源但的解码设备。 请参阅[声明旧资源](claiming-legacy-resources.md)有关详细信息。

微型端口后加载驱动程序并将其[ *HwVidInitialize* ](https://msdn.microsoft.com/library/windows/hardware/ff567345)函数运行时，微型端口驱动程序[ *HwVidStartIO* ](https://msdn.microsoft.com/library/windows/hardware/ff567367)函数调用以将映射的微型端口驱动程序将使其相应的显示器驱动程序的可见的视频内存的任何访问范围。

 

 





