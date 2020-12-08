---
title: AVStream 中的硬件编解码器支持入门
description: AVStream 中的硬件编解码器支持入门
keywords:
- 硬件编解码器支持 WDK AVStream，使用
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7d3aff21fcea95926ce427cdc37f781728ed305a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815831"
---
# <a name="getting-started-with-hardware-codec-support-in-avstream"></a>AVStream 中的硬件编解码器支持入门

从 Windows 7 开始， [windows 媒体基础](/windows/win32/medfound/media-foundation-programming-guide) 将基于 AVStream 的媒体组件表示为用户模式媒体基础转换 (MFTs) 。

通过使用此功能，供应商可以将基于硬件的解码器、编码器和视频处理器作为 MFTs 提供，进而可以在应用程序级别进行操作。

Windows 7 中的 AVStream 模型保持不变，只需对微型驱动程序进行少量的添加即可启用此功能。

下图显示了转码拓扑：

![说明转码拓扑的示意图](images/hw-transcoding.png)

为了获得最佳性能，关系图底部行中显示的媒体处理应在专用硬件中出现。 在此方案中，专用的转码硬件被称为 "受保护的硬件编码器解码器" (舍弃) 。 可以将舍弃打包为主板的插件模块或显示适配器上的集成功能。

Windows 7 仍然支持基于软件的转码。 但是，因为系统在专用硬件（而不是 CPU）上执行转码，所以，基于舍弃的解决方案可显著提高用户体验与基于软件的解决方案的比较。

如前面的关系图中所示，用户模式客户端可以使用在每个 MFT 上公开的 IMFTransform 接口访问用户模式转换。 IMFTransform 在 Vista 和更高版本的 Windows 中可用，但仅从 Windows 7 开始，才能向用户模式应用程序公开基于硬件的媒体处理机制。

系统提供的设备代理或 Devproxy 模块在 DirectShow 流式处理模型中的角色与 KSProxy 相同。 Devproxy 在用户模式下的内核模式和 MFT 组件中 *Ks.sys* 之间进行代理通信。

生成的包装硬件媒体处理功能称为设备代理 MFT。 若要利用此机制，AVStream 微型驱动程序应该执行以下操作：

- 将转换函数公开为作为 AVStream 微型驱动程序一部分的单个 KS 筛选器。 例如，如果设备具有解码、编码和视频处理功能，则这些函数应表示为三个不同的 KS 筛选器。

  - **编码器**：用于将未压缩格式转换为压缩格式。

  - **解码器**：用于从压缩格式转换为非压缩格式，其中必须包含 NV12。

  - **视频处理器**：用于执行缩放、隔行扫描/取消隔行扫描和格式转换。 请勿在解码器或编码器筛选器中包括视频处理支持。

    Microsoft 强烈建议供应商提供基于硬件的缩放支持。 但是，如果选择不提供基于硬件的缩放支持，则可以使用系统提供的视频处理 MFT 以降低性能级别执行缩放操作。 如果未提供基于硬件的缩放支持，则媒体基础拓扑生成器会自动将系统提供的缩放 MFT 插入到拓扑中。

- 在 Windows 7 和更高版本的 Windows 中提供的以下 KS 类别之一注册其媒体处理 KS 筛选器：

  - [**KSMFT \_ 类别 \_ 视频 \_ 解码器**](../install/ksmft-category-video-decoder.md)

  - [**KSMFT \_ 类别 \_ 视频 \_ 编码器**](../install/ksmft-category-video-encoder.md)

  - [**KSMFT \_ 类别 \_ 视频 \_ 处理器**](../install/ksmft-category-video-processor.md)

  - [**KSMFT \_ 类别 \_ 音频 \_ 解码器**](../install/ksmft-category-audio-decoder.md)

  - [**KSMFT \_ 类别 \_ 音频 \_ 编码器**](../install/ksmft-category-audio-encoder.md)

  此外，还定义了以下类别以用于其他转码方案：

  - [**KSMFT \_ 类别 \_ 视频 \_ 效果**](../install/ksmft-category-video-effect.md)

  - [**KSMFT \_ 类别多路复用器 \_**](../install/ksmft-category-multiplexer.md)

  - [**KSMFT \_ 类别的 \_ 信号分离器**](../install/ksmft-category-demultiplexer.md)

  - [**KSMFT \_ CATEGORY \_ 音频 \_ 效果**](../install/ksmft-category-audio-effect.md)

  - [**\_其他 KSMFT 类别 \_**](../install/ksmft-category-other.md)

- 媒体基础应用程序随后可以使用 [MFTEnumEx](/windows/win32/api/mfapi/nf-mfapi-mftenumex) 函数来枚举使用前面提到的类别注册为 MFTs 的设备。
