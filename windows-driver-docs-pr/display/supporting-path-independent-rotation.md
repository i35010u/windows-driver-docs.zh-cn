---
title: 支持独立于路径的旋转
description: 操作系统从 Windows 8.1 更新开始，横向优先显示最大可能的解决方法与上支持克隆纵向优先显示。
ms.assetid: 136CEDA5-2839-4E6E-A032-1A9222C769C6
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 95eceac4bc6d2091b7e67c82d4db142d6bc6b728
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350177"
---
# <a name="span-iddisplaysupportingpath-independentrotationspansupporting-path-independent-rotation"></a><span id="display.supporting_path-independent_rotation"></span>支持独立于路径的旋转


操作系统从 Windows 8.1 更新开始，横向优先显示最大可能的解决方法与上支持克隆纵向优先显示。 显示微型端口驱动程序必须设置适当的偏移量的值[ **D3DKMDT\_VIDPN\_存在\_路径\_旋转\_支持**](https://msdn.microsoft.com/library/windows/hardware/ff546705)结构*主克隆路径*并*辅助克隆路径*，如中所述[显示微型端口驱动程序中支持旋转](supporting-rotation-in-a-display-miniport-driver.md)。

这些设备驱动程序接口 (DDIs) 是 Windows 8.1 更新中的新增功能：

-   D3DKMDT_VPPR_GET_CONTENT_ROTATION
-   D3DKMDT_VPPR_GET_CONTENT_ROTATION_PART
-   D3DKMDT_VPPR_GET_OFFSET_ROTATION

在 Windows 8.1 更新中更新这些 DDIs:

-   [**D3DKMDT\_VIDPN\_存在\_路径\_旋转\_支持**](https://msdn.microsoft.com/library/windows/hardware/ff546705)

-   [**D3DKMDT\_VIDPN\_存在\_路径\_旋转**](https://msdn.microsoft.com/library/windows/hardware/ff546700)

## <a name="span-idcloningaportrait-firstdevicespanspan-idcloningaportrait-firstdevicespanspan-idcloningaportrait-firstdevicespancloning-a-portrait-first-device"></a><span id="Cloning_a_portrait-first_device"></span><span id="cloning_a_portrait-first_device"></span><span id="CLONING_A_PORTRAIT-FIRST_DEVICE"></span>克隆纵向第一个设备


当请求的纵向第一个设备驱动程序时要克隆到横向第一个监视器时，它应该报告源模式 (*x*，*y*) 匹配主克隆路径中的解决方法的解决方法。 辅助克隆路径无法再支持 90 和 270 度偏移量的值 ([**D3DKMDT\_VIDPN\_存在\_路径\_旋转\_支持**](https://msdn.microsoft.com/library/windows/hardware/ff546705).**Offset90**或。**Offset270**都**TRUE**)。 因此，当 VidPN 是与提交[ **D3DKMDT\_VIDPN\_存在\_路径\_旋转**](https://msdn.microsoft.com/library/windows/hardware/ff546700)枚举值，该值指示 90-或 270-程度偏移量，这意味着，(*x*，*y*) 在此特定路径中翻转的解决方法。

默认情况下在操作系统中选择辅助克隆路径为内部显示面板。 在内部面板是纵向的第一，操作系统要求的情况下[ **D3DKMDT\_VIDPN\_存在\_路径\_旋转\_支持**](https://msdn.microsoft.com/library/windows/hardware/ff546705).**Offset270**若要在此路径上设置以在横向模式中内部显示面板上显示。 对于横向第一个外部监视器辅助克隆路径中，操作系统需要的驱动程序以支持**D3DKMDT\_VIDPN\_存在\_路径\_旋转\_支持**。**Offset90**，尽管这很可能是少见的方案。

## <a name="span-idexampleclonescenariosspanspan-idexampleclonescenariosspanspan-idexampleclonescenariosspanexample-clone-scenarios"></a><span id="Example_clone_scenarios"></span><span id="example_clone_scenarios"></span><span id="EXAMPLE_CLONE_SCENARIOS"></span>示例克隆方案


下面是一个典型的方案，其中具有自身分辨率为 800 （宽度） x 1280 像素 （高度） 的纵向第一个设备连接到使用高度 1080年像素的横向第一个电视克隆模式中。 该驱动程序会给系统报告此信息：

<span id="source_mode"></span><span id="SOURCE_MODE"></span>源模式  
1280 x 800

<span id="TV_target_mode"></span><span id="tv_target_mode"></span><span id="TV_TARGET_MODE"></span>电视目标模式  
1920 x 1080 （缩放保留纵横比）

<span id="device_target_mode"></span><span id="DEVICE_TARGET_MODE"></span>设备目标模式  
800 x 1280 （标识缩放）

<span id="primary_clone_path__TV_"></span><span id="primary_clone_path__tv_"></span><span id="PRIMARY_CLONE_PATH__TV_"></span>主要克隆路径 （电视）  
驱动程序仅支持[ **D3DKMDT\_VIDPN\_存在\_路径\_旋转\_支持**](https://msdn.microsoft.com/library/windows/hardware/ff546705)。**Offset0**，以及正常方式轮换的支持

<span id="secondary_clone_path__device_"></span><span id="SECONDARY_CLONE_PATH__DEVICE_"></span>辅助克隆路径 （设备）  
驱动程序仅支持[ **D3DKMDT\_VIDPN\_存在\_路径\_旋转\_支持**](https://msdn.microsoft.com/library/windows/hardware/ff546705)。**Offset270**，以及正常方式轮换的支持

<span></span>  

在调用[ *DxgkDdiCommitVidPn* ](https://msdn.microsoft.com/library/windows/hardware/ff559597)函数将这些路径中的设置然后返回[ **D3DKMDT\_VIDPN\_存在\_路径\_旋转**](https://msdn.microsoft.com/library/windows/hardware/ff546700)枚举：

<span id="primary_clone_path__TV_"></span><span id="primary_clone_path__tv_"></span><span id="PRIMARY_CLONE_PATH__TV_"></span>主要克隆路径 （电视）  
**D3DKMDT\_VPPR\_IDENTITY**

<span id="secondary_clone_path__device_"></span><span id="SECONDARY_CLONE_PATH__DEVICE_"></span>辅助克隆路径 （设备）  
**D3DKMDT\_VPPR\_IDENTITY\_OFFSET270**

操作系统需要的驱动程序来旋转 270 度提供的内容。

如果在**显示**控制面板中的**方向**下拉列表框中，用户选择**横向 （翻转）** 选项，调用[ *DxgkDdiCommitVidPn* ](https://msdn.microsoft.com/library/windows/hardware/ff559597)函数将返回具有从这些路径设置[ **D3DKMDT\_VIDPN\_存在\_路径\_旋转**](https://msdn.microsoft.com/library/windows/hardware/ff546700)枚举：

<span id="primary_clone_path__TV_"></span><span id="primary_clone_path__tv_"></span><span id="PRIMARY_CLONE_PATH__TV_"></span>主要克隆路径 （电视）  
**D3DKMDT\_VPPR\_ROTATE180**

<span id="secondary_clone_path__device_"></span><span id="SECONDARY_CLONE_PATH__DEVICE_"></span>辅助克隆路径 （设备）  
**D3DKMDT\_VPPR\_ROTATE180\_OFFSET270**

如果桌面窗口管理器 (DWM) 已具有旋转 180 度的内容，该驱动程序必须仍将其旋转辅助克隆路径中的另一个 270 度。 否则，该驱动程序必须旋转 180 度的电视和 90 度的设备的内容。 请注意，若要旋转内容，该驱动程序必须设置**旋转**的成员[ **DXGK\_PRESENTFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff562005)结构。

 

 





