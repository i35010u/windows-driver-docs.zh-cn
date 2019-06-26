---
title: DXGI 呈现路径
description: DXGI 呈现路径
ms.assetid: 3519172d-261c-4b33-b1e7-c4abf33b15f3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f907f9ac6cc3dd085db32a10f347c1bc4891e26
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355018"
---
# <a name="dxgi-presentation-path"></a>DXGI 呈现路径


DXGI 为应用程序的演示文稿方法提供该"确实行得通"。 例如，应用程序不需要执行任何特殊操作窗口模式和全屏模式之间进行切换。 此演示文稿的方法是可能的因为 DXGI 和用户模式显示驱动程序协同工作，以便跨组合的多个采样抗锯齿 (MSAA) 中，监视器旋转回和前台缓冲区之间的差异大小和格式，保留演示文稿和全屏幕与有窗口的模式。 DXGI 的另一个优点是它允许以具有有限的功能来扫描扩展 MSAA 和旋转图面，因为 DXGI 提供了"无状态"DDI 的显示适配器。 无状态 DDI 中适配器的驱动程序不需要记录在 DDI 调用之间的数据。

演示文稿的基本任务是将数据从呈现的后台缓冲区移到主图面进行查看。 以下各节所述在不同情况下执行此任务。

### <a name="span-idwindowedmodewithdwmonspanspan-idwindowedmodewithdwmonspanwindowed-mode-with-dwm-on"></a><span id="windowed_mode_with_dwm_on"></span><span id="WINDOWED_MODE_WITH_DWM_ON"></span>使用 DWM 上窗口模式

在窗口模式下与桌面 Windows 管理器 (DWM)-上的情况下，DXGI 与 DWM 进行通信，并打开的共享资源是 DXGI 生成者的呈现器目标和 DWM 的纹理的视图。 除了应用程序会创建任何后台缓冲区存在此共享的资源。 DXGI 调用驱动程序的[ **BltDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数将数据从任何后缓冲到共享图面。 此操作可能需要拉伸，颜色转换并 MSAA 解决。 但是，此操作永远不会需要源和目标子矩形。 事实上，不能对的调用中表示这些子矩形*BltDXGI*。 此位块传输 (bitblt) 始终具有**存在**中设置标志**标志**的成员[ **DXGI\_DDI\_ARG\_BLT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_blt)结构的*pBltData*参数指向。 设置**存在**标志指示驱动程序应以原子方式执行该操作。 该驱动程序执行的 bitblt 操作以原子方式撕裂现象的可能性降至 DWM 组合的共享的资源中读取数据时。

### <a name="span-idwindowedmodewithdwmoffspanspan-idwindowedmodewithdwmoffspanwindowed-mode-with-dwm-off"></a><span id="windowed_mode_with_dwm_off"></span><span id="WINDOWED_MODE_WITH_DWM_OFF"></span>使用 DWM 关闭窗口模式

在与 DWM 关闭用例窗口模式下，DXGI 调用驱动程序的[ **PresentDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数与**Blt**中设置标志**标志**成员[ **DXGI\_DDI\_ARG\_存在**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_present)结构*pPresentData*参数所指向自。 在此*PresentDXGI*调用时，DXGI 可以指定任何在应用程序创建的后台缓冲区**hSurfaceToPresent**并**SrcSubResourceIndex** DXGI的成员\_DDI\_ARG\_存在。 没有任何其他共享图面。

### <a name="span-idfullscreenmodespanspan-idfullscreenmodespanfull-screen-mode"></a><span id="full_screen_mode"></span><span id="FULL_SCREEN_MODE"></span>全屏幕模式

全屏显示用例是比使用 DWM 打开或关闭窗口模式更为复杂。

当 DXGI 可以过渡到全屏幕模式下时，它会尝试利用以减少带宽并获得垂直同步同步翻转操作。 以下条件下可以不使用翻转操作：

-   应用程序没有重新分配一种方法，它们与匹配主图面中的其后台缓冲区。

-   该驱动程序指定，它将不扫描扩展后台缓冲区 （例如，因为后台缓冲区进行旋转或 MSAA）。

-   指定应用程序，它不能接受 Direct3D 运行时放弃的后台缓冲区的内容，并请求 （总计） 链中的只有一个缓冲区。 (在这种情况下，DXGI 分配后面和主面; 但 DXGI 使用驱动程序的*PresentDXGI*起作用**Blt**标志设置。)

翻转操作和对驱动程序的调用，从而防止发生上述条件之一时[ **PresentDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数与**Blt**标志设置也是不适当的 （因为后台缓冲区不完全匹配前台缓冲区），DXGI 分配*代理面*。 此代理面匹配前台缓冲区。 因此，代理面和前台缓冲区之间翻转成为可能。 如果存在代理图面，DXGI 使用驱动程序的[ **BltDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数与**存在**标记清除 (0) 将应用程序的后台缓冲区复制到代理图面。 在此*BltDXGI*调用时，DXGI 可能请求转换、 拉伸，和解析。 DXGI 然后调用驱动程序的*PresentDXGI*起作用**翻转**中设置标志**标志**隶属[ **DXGI\_DDI\_ARG\_存在**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_present)结构移动代理图面上 bits 来扫描扩展。

若要通知驱动程序可以从扫描出选择退出的用户模式显示驱动程序，驱动程序将收到扫描出应用层协议的可选和非可选类创建资源时调用。 可选扫描出表面指定通过 dxgi 紧密\_DDI\_主\_可选标志。 非可选扫描扩展图面没有 DXGI\_DDI\_主\_可选标志设置。 有关创建资源时调用这些类型的详细信息，请参阅[可以在资源创建时将传递 DXGI 信息](passing-dxgi-information-at-resource-creation-time.md)。

DXGI 设置 DXGI\_DDI\_主\_可选标志，以重新创建所有缓冲图面 （即，可选图面），并且未设置任何前缓冲区或代理图面 （即，非可选面） 的标志。

如果 DXGI\_DDI\_主\_可选设置后，该缓冲区，该驱动程序可以设置 DXGI\_DDI\_主\_驱动程序\_标志\_没有\_SCANOUT 标志。 有关设置此标志的详细信息，请参阅[可以在资源创建时将传递 DXGI 信息](passing-dxgi-information-at-resource-creation-time.md)。 如果驱动程序设置 DXGI\_DDI\_主\_驱动程序\_标志\_否\_SCANOUT 可选缓冲区，它不起作用而不会导致 DXGI 调用驱动程序的[**PresentDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)起作用**Blt**标记而不是设置与**翻转**标志设置。

如果 DXGI\_DDI\_主\_可选未设置为前台缓冲区或代理图面，该驱动程序仍可以通过失败，错误代码为 DXGI 资源创建调用选择退出扫描扩展\_DDI\_ERR\_不受支持并设置 DXGI\_DDI\_主\_驱动程序\_标志\_否\_SCANOUT。

**请注意**  失败创建调用，而无需设置 DXGI\_DDI\_主\_驱动程序\_标志\_否\_为真正的故障情况下，保留 SCANOUT如内存不足。

 

尝试为 MSAA 或旋转的后台缓冲区创建全屏显示链时，DXGI 利用此选择退出方法。 如果该驱动程序将不扫描扩展中任何或这两种类型，该驱动程序将选择退出。然后，DXGI 将尝试创建非旋转图面、 一个非 MSAA 表面上，或两者，直到该驱动程序接受创建资源。 因此，DXGI 将回退以渐进方式直到非可选面与前台缓冲区格式、 抽样计数、 旋转和大小完全匹配。

如果该驱动程序选择不使用任何非可选的图面，DXGI 仍必须具有一种方法将从后台缓冲区的位移动到主图面。 因此，如果驱动程序选择不使用 MSAA 和旋转的扫描的超时，该驱动程序选择启用解析、 轮换，或这两者时 DXGI 调用驱动程序的[ **BltDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数。 DXGI 时驱动程序选择，将创建一个代理图面，然后调用**BltDXGI**将数据从后台缓冲区移到该代理图面。 该驱动程序应具有无需选择退出此代理面因为代理与前台缓冲区完全匹配。

应用程序不会重新创建其图面后转换传入或传出的全屏模式下时，可能发生以下异常情况：

-   如果应用程序不会重新创建其图面时，它将进入全屏模式下，DXGI 确定后台缓冲区不会匹配前缓冲，即使它们实际上匹配上格式、 大小、 旋转和样本计数。 此决定的原因是操作系统需要后台缓冲区来标记用于扫描扩展到特定监视器创建这些缓冲区时。 有窗口的后台缓冲区无法尚未将明确分配给特定监视器因为监视器进入全屏显示时动态选择。 因此，DXGI 不必须将这些后台缓冲区发送到扫描扩展 （通过翻转操作） 的驱动程序。 此类型的应用程序通常强制 DXGI 创建代理图面。

-   如果它返回到窗口模式时，应用程序不会重新创建其后台缓冲区，DXGI 可能调用的驱动程序[ **BltDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)或[ **PresentDXGI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) (使用**Blt**设置) 来执行 bitblt 先前为翻转操作创建的表面上。 这种情况下应不会出现问题，但出于完整性的考虑此处提及。 请注意 DXGI 始终销毁代理图面，当应用程序转换到窗口模式。

另请注意应用程序可以动态调整其后台缓冲区，在应用程序在全屏幕模式下时。 此操作导致所述的逻辑在上述情况下再次发生。 因此，可能会创建和销毁时，代理面并选择禁用可能会或可能不需要随着时间的推移即使在应用程序保持在全屏幕模式下也是如此。 应用程序还可以转移其输出到另一个监视器动态而无需离开的全屏模式。 因此，应用程序会切换回 bitblt 模式，因为应用程序的后台缓冲区被标记为另一个监视器。

最后，您应注意如果驱动程序不会选择不向外 MSAA 扫描相对于 MSAA 后台缓冲区会发生这种情况。在此情况下，该驱动程序选择启用 MSAA 扫描带。 因此，DXGI 交换缓冲区和 MSAA 前台缓冲区通过回复 MSAA 翻转操作，并按等效于数字模拟转换器 (DAC) 执行解析操作。 在这种情况下，应用程序可以调整大小动态地在全屏幕模式下，这会强制 DXGI，若要切换到调用的驱动程序及其后缓冲[ **BltDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数。 由于后台缓冲区和前台缓冲区的 MSAA 特征仍然匹配，DXGI 将指定驱动程序执行非解决，可能将颜色转换，拉伸 bitblt。 而无需解析，则驱动程序应再复制到前台缓冲区，如果驱动程序将选择要扫描扩展 MSAA，则需要多样本。

 

 





