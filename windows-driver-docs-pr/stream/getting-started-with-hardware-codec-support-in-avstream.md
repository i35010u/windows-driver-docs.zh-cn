---
title: AVStream 中的硬件编解码器支持入门
description: AVStream 中的硬件编解码器支持入门
ms.assetid: f8335285-e74f-4600-aee9-7e2881cb0764
keywords:
- 硬件编解码器支持 WDK AVStream 使用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e21751d64eac49db8337e789474709134f08782
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363624"
---
# <a name="getting-started-with-hardware-codec-support-in-avstream"></a>AVStream 中的硬件编解码器支持入门


在 Windows 7 中，启动[Windows Media Foundation](https://go.microsoft.com/fwlink/p/?linkid=155069) AVStream 基于媒体组件表示为用户模式下媒体基础转换 (Mft)。

通过使用此功能，供应商可以为又可以在应用程序级别操作的 Mft 提供基于硬件的解码器和编码器，视频处理器。

AVStream 模型保持不变，在 Windows 7 中，需要为微型驱动程序以启用此功能仅几个新增功能。

在下图显示了转码拓扑：

![关系图演示转码拓扑](images/hw-transcoding.png)

为了获得最佳性能，关系图的底部行中所示的媒体处理应发生在专用硬件。 在此方案中，专用的转码硬件称为作为保护硬件编码器解码器 （工棚）。 为主板的插件模块或显示适配器上的一集成功能，可打包工棚。

Windows 7 仍然支持基于软件的转码。 但是，由于系统而不是 CPU 的专用硬件上执行的代码转换工作，因此基于工棚的解决方案可以提高显著与基于软件的解决方案的用户体验。

上面的关系图中所示，用户模式下客户端可以访问每个 MFT 上使用 IMFTransform 界面公开用户模式转换。 IMFTransform 目前在 Vista 和更高版本的 Windows，但只能从 Windows 7 开始，提供的机制来公开基于硬件的媒体处理-用户模式应用程序。

系统提供的设备代理或 Devproxy，模块提供与 KSProxy DirectShow 流式处理模型中相同的角色。 Devproxy 中转站之间的通信*Ks.sys*在内核模式下和在用户模式下的 MFT 组件中。

生成的已包装的硬件媒体处理函数称为设备代理 MFT。 若要利用此机制，AVStream 微型驱动程序应执行以下操作：

-   将转换函数公开为属于 AVStream 微型驱动程序的单个 KS 筛选器。 例如，如果设备已解码，编码，而且视频处理功能，这些函数应表示为三个非重复 KS 筛选器。
    -   **编码器**： 用于从非压缩格式转换为以压缩格式。
    -   **解码器**： 用于从压缩格式转换为压缩的格式，其中必须包括 NV12。
    -   **视频处理器**： 用于执行缩放、 交错/de-隔行扫描，以及格式转换。 解码器或编码器筛选器中不包括视频处理支持。

        Microsoft 强烈建议供应商提供基于硬件的缩放支持。 但是，如果您选择不提供基于硬件的缩放支持，您可以使用系统提供的视频处理 MFT 执行级别的性能降低的缩放操作。 如果未提供基于硬件的缩放支持，Media Foundation 拓扑生成器会自动将系统提供的缩放 MFT 插入到拓扑。

-   注册其媒体处理 KS 下一个以下 KS 类别，在 Windows 7 和更高版本的 Windows 中可用的筛选器：

    -   [**KSMFT\_CATEGORY\_VIDEO\_DECODER**](https://msdn.microsoft.com/library/windows/hardware/ff548602)
    -   [**KSMFT\_CATEGORY\_VIDEO\_ENCODER**](https://msdn.microsoft.com/library/windows/hardware/ff548611)
    -   [**KSMFT\_CATEGORY\_VIDEO\_PROCESSOR**](https://msdn.microsoft.com/library/windows/hardware/ff548613)
    -   [**KSMFT\_CATEGORY\_AUDIO\_DECODER**](https://msdn.microsoft.com/library/windows/hardware/ff548572)
    -   [**KSMFT\_CATEGORY\_AUDIO\_ENCODER**](https://msdn.microsoft.com/library/windows/hardware/ff548584)

    此外，还用于其他代码转换方案中定义以下类别：

    -   [**KSMFT\_CATEGORY\_VIDEO\_EFFECT**](https://msdn.microsoft.com/library/windows/hardware/ff548607)
    -   [**KSMFT\_类别\_复用器**](https://msdn.microsoft.com/library/windows/hardware/ff548596)
    -   [**KSMFT\_类别\_信号分离器**](https://msdn.microsoft.com/library/windows/hardware/ff548594)
    -   [**KSMFT\_CATEGORY\_AUDIO\_EFFECT**](https://msdn.microsoft.com/library/windows/hardware/ff548578)
    -   [**KSMFT\_类别 \_ /伙伴**](https://msdn.microsoft.com/library/windows/hardware/ff548601)
-   然后，Media foundation 应用程序可以使用[MFTEnumEx](https://go.microsoft.com/fwlink/p/?linkid=155058)函数合用来枚举作为 Mft 情况下通过使用前面提到的类别已注册的设备。

 

 




