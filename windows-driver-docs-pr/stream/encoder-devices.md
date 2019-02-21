---
title: 编码器设备
description: 编码器设备
ms.assetid: 156b1d6d-c6f6-4ab3-a91e-3124351c6ae5
keywords:
- 编码器设备 WDK AVStream
- AVStream WDK，编码器设备
- 未压缩数据流 WDK AVStream
- 编码的流 WDK AVStream
- 音频编码器设备 WDK AVStream
- 视频编码器设备 WDK AVStream
- 基于软件的编码器 WDK AVStream
- 基于硬件的编码器 WDK AVStream
- 集成的编码器 WDK AVStream
- 独立编码器 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecaf4ff2257f0a6efb9c47d99158fbf2530a4733
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533985"
---
# <a name="encoder-devices"></a>编码器设备





编码器是收到作为输入 （视频和/或音频） 的未压缩的数据流，将流编码为特定的格式，如 MPEG2，以及然后输出编码的流的设备。 编码器设备可能属于另一个设备，如组合电视调谐器/捕获适配器，或者它们可能单独。 例如，集成的编码器的捕获设备，如模拟电视调谐器/解码器从接收数据流，然后生成编码的流。 独立编码器可能会接收未压缩文件的输入的数据、 处理数据，然后输出编码数据。

Microsoft 的基于硬件的音频/视频编码器设备在 DirectX 9.0 和更高版本提供支持。 DirectX 9.0 可再发行组件现在可供以下 Microsoft Windows 平台：

-   Windows Media Center Edition 2004

-   Windows Server 2003

-   Windows XP Home 和 Professional

-   Windows 2000 Professional 和 Server

-   Windows Millennium Edition

-   Windows 98 Second Edition

若要支持音频/视频编码器设备，必须在内核流式处理筛选器微型驱动程序中实现对 Microsoft 定义编码器属性的支持。 支持可能通过实现编码器属性添加到现有的流类或 AVStream 微型驱动程序。 或者，如果你正在编写新微型驱动程序 （无论是用于独立编码器） 或一个集成，Microsoft 建议您按照 AVStream 体系结构因为流类已过时，不再受支持。 可以使用[AVStream 模拟硬件示例驱动程序 (Avshws)](https://go.microsoft.com/fwlink/p/?LinkId=618052)作为起始点。 Avshws 驱动程序是实现支持 DMA 传输的一个 pin 构建以 AVStream 示例。

**请注意**  如果你正在编写软件实现的编码器，则不应将其编写为流式处理筛选器内核。 相反，应为 Microsoft DirectShow 筛选器或 DirectX 媒体对象编写此类筛选器。 请参阅有关基于软件的编码器的详细信息的 DirectShow SDK 主题"编码器 API"。

 

客户端访问通过编码器功能[ **ICodecAPI** ](https://msdn.microsoft.com/library/windows/desktop/dd311953) COM 接口。 您指定 KsProxy 在驱动程序的 INF 文件，具体取决于属性中公开的接口实现了您微型驱动程序。 请参阅[编码器实现和支持](encoder-implementation-and-support.md)有关 Microsoft 定义内核流式处理属性和事件。 请参阅[编码器的代码示例](encoder-code-examples.md)有关如何实现它们的示例。 请参阅[编码器安装和注册](encoder-installation-and-registration.md)有关如何安装编码器筛选器的信息，包括如何指定 KsProxy 应公开的 COM 接口。

编码器设备必须符合 Windows 认证计划除了涵盖所有设备的通用徽标要求中所述的流式处理媒体和广播要求。

 

 




