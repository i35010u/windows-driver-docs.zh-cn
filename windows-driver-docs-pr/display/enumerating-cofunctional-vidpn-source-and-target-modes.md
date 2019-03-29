---
title: 枚举协同工作的 VidPN 源和目标模式
description: 枚举协同工作的 VidPN 源和目标模式
ms.assetid: f1aa6277-7af6-4ba0-8ff1-d562f7029540
keywords:
- 视频存在 WDK 显示的网络，则枚举目标和源模式
- VidPN WDK 显示枚举目标和源模式
- 约束 VidPN WDK
- 枚举目标和源模式 WDK 视频存在网络
- 源模式 WDK 视频存在网络
- 目标模式 WDK 视频存在网络
- 固定缩放转换 WDK 视频存在网络
- 固定旋转转换 WDK 视频存在网络
- 多级取样方法 WDK 视频存在网络
- 模式可设置 WDK 视频存在网络
- 检查约束 VidPN WDK
- 缩放支持标志 WDK 视频存在网络
- 旋转支持标志 WDK 视频存在网络
- 枚举透视 WDK 视频存在网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9599e9fcf89c09a0f8b7993989e395596b0a9f1d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564824"
---
# <a name="enumerating-cofunctional-vidpn-source-and-target-modes"></a>枚举协同工作的 VidPN 源和目标模式


本主题介绍视频存在网络 (VidPN) 管理器和显示微型端口驱动程序的协作方式枚举在视频显示源和目标上可用的模式。 在阅读此材料之前, 应该熟悉以下主题中的材料：

-   [简介视频存在网络](introduction-to-video-present-networks.md)

-   [VidPN 对象和接口](vidpn-objects-and-interfaces.md)

有时，VidPN 经理要求显示微型端口驱动程序来枚举显示适配器的视频显示源和目标上可用的模式。 通常情况下，该请求具有以下模式：

1.  VidPN 管理器创建或获取 VidPN 一些，但其源和目标的不是全部，具有固定的模式。

2.  VidPN 管理器调用[ **DxgkDdiIsSupportedVidPn** ](https://msdn.microsoft.com/library/windows/hardware/ff559684)以确定是否可以扩展 VidPN 以窗体显示适配器支持的功能 VidPN。 也就是说，它会要求剩余的源和目标上而无需更改现有的固定的模式是否可以固定模式。

3.  VidPN 管理器调用[ **DxgkDdiEnumVidPnCofuncModality** ](https://msdn.microsoft.com/library/windows/hardware/ff559649)若要获取的源和目标，尚不具有固定模式上可用的模式。

一个参数传递给*DxgkDdiEnumVidPnCofuncModality*是名为约束 VidPN VidPN 对象的句柄。

*DxgkDdiEnumVidPnCofuncModality*必须执行以下操作：

-   检查约束 VidPN。

-   对于每个源和目标不具有固定的模式下，调整将模式设置，这样就具有约束同时正常工作的最大可能的模式集。

-   对于不具有固定缩放转换每个路径，调整缩放支持标志，以便可以同时具有约束正常工作。

-   对于没有固定的旋转转换，旋转角度的调整每个路径支持标志，以便它们同时具有约束正常工作。

-   对于每个源具有固定的模式下，报表可用于该源多级取样方法。

以下各段提供有关如何在前一项目符号列表中执行每个任务的详细信息。

### <a name="span-idinspectingtheconstrainingvidpnspanspan-idinspectingtheconstrainingvidpnspaninspecting-the-constraining-vidpn"></a><span id="inspecting_the_constraining_vidpn"></span><span id="INSPECTING_THE_CONSTRAINING_VIDPN"></span>检查约束 VidPN

约束 VidPN 的以下属性是必须遵循的约束*DxgkDdiEnumVidPnCofuncModality*。

-   拓扑 （源和目标之间的关联组）

-   固定的模式

-   缩放调整每个路径的支持、 旋转和旋转的支持

-   每个路径的目标的颜色基础

-   每个路径的动态目标颜色系数的范围

-   每个路径的内容类型 （图形或视频）

-   Gamma 负载增加的每个路径

若要从约束 VidPN 提取约束，请执行以下步骤：

-   首先调用[ **pfnGetTopology** ](https://msdn.microsoft.com/library/windows/hardware/ff562854)函数以获取指向的指针[VidPN 拓扑接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)表示约束 VidPN 的拓扑。

-   调用[ **pfnAcquireFirstPathInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff562092)并[ **pfnAcquireNextPathInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff562093)函数来获取有关每个路径中的信息约束 VidPN 的拓扑。 有关特定路径 （源 ID、 目标 ID，缩放转换、 旋转转换、 目标颜色基础等） 的信息包含在[ **D3DKMDT\_VIDPN\_存在\_路径** ](https://msdn.microsoft.com/library/windows/hardware/ff546647)结构。

-   为每个路径的路径的源将 ID 传递到[ **pfnAcquireSourceModeSet** ](https://msdn.microsoft.com/library/windows/hardware/ff562110)函数以获取路径的源。

-   调用[ **pfnAcquirePinnedModeInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff562076)函数来确定哪种模式 （如果有） 固定在源的模式设置。 如果源的模式设置具有固定的模式，则可能无需检查组中的剩余模式。 如果模式设置不具有固定的模式下，通过调用检查组中的剩余模式[ **pfnAcquireFirstModeInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff562074)并[ **pfnAcquireNextModeInfo**](https://msdn.microsoft.com/library/windows/hardware/ff562075).

    检查目标模式集并确定哪些目标模式集具有固定模式，请使用类似的步骤。

### <a name="span-idadjustingmodesetsspanspan-idadjustingmodesetsspanadjusting-mode-sets"></a><span id="adjusting_mode_sets"></span><span id="ADJUSTING_MODE_SETS"></span>通过调整模式设置

因为检查与源和目标约束 VidPN 拓扑中的关联的模式集，请记下的哪一种模式集具有固定模式。 如果模式设置没有固定的模式下，确定它是否需要进行调整。 如果它包含不是同时具有约束正常工作的模式，或它缺少具有约束同时正常工作的可用模式，必须调整模式设置。

对于已连接监视器的视频存在目标，还必须考虑的一套由监视器支持的模式。 即使显示适配器上的视频显示目标支持 （给定的约束条件） 的特定模式，应仅列出在目标的模式下，如果已连接的监视器还支持模式，则设置该模式。 若要确定已连接监视器支持的模式，请执行以下步骤：

-   [DXGK\_监视器界面](https://msdn.microsoft.com/library/windows/hardware/ff561949)

    调用[ **pfnAcquireMonitorSourceModeSet**](https://msdn.microsoft.com/library/windows/hardware/ff561953)。 如果一种模式需要不设置不做任何调整，可以让它保持原状。 如果模式设置需要进行调整，然后必须创建一组新的模式，并替换为使用新设置的现有模式。

-   [DXGK_VIDPN_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)

    若要创建并填充新的源模式集，调用[ **pfnCreateNewSourceModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_createnewsourcemodeset)。

-   [_DXGK_VIDPNSOURCEMODESET_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface)

    然后调用[ **pfnCreateNewModeInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff562078)并[ **pfnAddMode**](https://msdn.microsoft.com/library/windows/hardware/ff562077)。

-   [DXGK_VIDPN_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)

    最后调用[ **pfnAssignSourceModeSet** ](https://msdn.microsoft.com/library/windows/hardware/ff562840)替换现有的源模式，使用新设置。

### <a name="adjusting-scaling-support-flags"></a>调整缩放支持标志

对于约束 VidPN 拓扑中每个路径，确定路径是否具有固定缩放转换。 若要做出决定，检查*vpnPath*。**ContentTransformation.Scaling**，其中*vpnPath*是[ **D3DKMDT\_VIDPN\_存在\_路径**](https://msdn.microsoft.com/library/windows/hardware/ff546647)结构，它表示的路径。 如果*vpnPath*。**ContentTransformation.Scaling**设置为**D3DKMDT\_VPPS\_标识**， **D3DKMDT\_VPPS\_居中**，或**D3DKMDT\_VPPS\_STRETCHED**，然后固定的缩放转换的路径。 否则，不被固定的缩放转换。

如果路径不具有固定缩放转换，确定是否需要进行调整的路径的缩放支持标志。 如果它们演示了对扩展的类型的支持不具有约束同时正常工作，或者如果它们无法显示对扩展的类型的支持是同时具有约束正常工作，必须进行调整的支持标志。 若要更改的缩放支持标志设置的成员[ **D3DKMDT\_VIDPN\_存在\_路径\_缩放\_支持**](https://msdn.microsoft.com/library/windows/hardware/ff546712)保存标志的结构。

### <a name="adjusting-rotation-support-flags"></a>调整旋转支持标志

调整路径的旋转支持标志是类似于调整路径的缩放支持标志。 假设*vpnPath*是 D3DKMDT\_VIDPN\_存在\_路径结构。 如果*vpnPath*。**ContentTransformation.Rotation**设置为**D3DKMDT\_VPPR\_标识**， **D3DKMDT\_VPPR\_ROTATE90**，**D3DKMDT\_VPPR\_ROTATE180**，或**D3DKMDT\_VPPR\_ROTATE270**，则该路径的旋转转换为固定。 否则，未固定在旋转转换。 旋转支持标志位于*vpnPath*。**ContentTransformation.RotationSupport**。

### <a name="span-idreportingmultisamplingmethodsspanspan-idreportingmultisamplingmethodsspanreporting-multisampling-methods"></a><span id="reporting_multisampling_methods"></span><span id="REPORTING_MULTISAMPLING_METHODS"></span>报告多级取样方法

如果显示适配器具有一个或多个输出视频编解码器的多重采样抗锯齿功能的支持的则必须为每个源都具有固定的模式报告 （对于约束），提供了的多级取样方法。 若要报告可用的多级取样方法，请执行以下步骤：

-   创建的数组[D3DDDI\_MULTISAMPLINGMETHOD](https://msdn.microsoft.com/library/windows/hardware/ff544594)结构
-   将数组传递给[ **pfnAssignMultisamplingMethodSet** ](https://msdn.microsoft.com/library/windows/hardware/ff562115)函数的[VidPN 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)。

[D3DDDI\_MULTISAMPLINGMETHOD](https://msdn.microsoft.com/library/windows/hardware/ff544594)结构具有两个成员，您必须将其设置，用于确定的特征的多级取样的方法。 **采样**成员指示 subpixels 进行采样的数目。 **NumQualityLevels**成员指示该方法可以执行操作的质量级别数。 只要级别中的每一项增加有明显改善显示的图像的质量，可以指定任意数量的质量级别。

### <a name="span-idenumerationpivotsspanspan-idenumerationpivotsspanenumeration-pivots"></a><span id="enumeration_pivots"></span><span id="ENUMERATION_PIVOTS"></span>枚举数据透视表

如前面所述*DxgkDdiEnumVidPnCofuncModality*必须创建与传入 VidPN 同时正常工作的模式集及其*hConstrainingVidPn*参数。 在某些情况下， *DxgkDdiEnumVidPnCofuncModality*必须增加 (枚举 pivot) 的其他信息根据传入其行为*EnumPivotType*和*EnumPivot*参数。

枚举透视可以是以下值之一：

-   特定的视频显示源模式设置

-   特定的视频显示目标模式设置

-   特定的 VidPN 显示路径缩放转换

-   特定的 VidPN 显示路径旋转转换

如果枚举透视是一模式，则*DxgkDdkEnumVidPnCofuncModality*必须保留该模式设置不变。 如果枚举透视的缩放 （旋转） 转换的路径，然后*DxgkDdiEnumVidPnCofuncModality*不得更改该路径的缩放 （旋转） 支持标志。

 

 





