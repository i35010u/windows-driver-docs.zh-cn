---
title: Windows 中的 DVD 解码器支持
description: Windows 中的 DVD 解码器支持
ms.assetid: 3a77b6d1-6095-4cf8-8cd4-2e6d80d171c8
keywords:
- DVD 解码器微型驱动程序 WDK，Windows 支持
- 解码器微型驱动程序 WDK DVD，Windows 支持
- DVD 解码器微型驱动程序 WDK，写入
- 解码器微型驱动程序 WDK DVD，写入
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 446845b6d4c2c3f9746962bea6b564963cfd70ed
ms.sourcegitcommit: b481c9513a9ea7f824ecabd1ae18876548032252
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879030"
---
# <a name="dvd-decoder-support-in-windows"></a>Windows 中的 DVD 解码器支持

> [!NOTE]
> 本主题适用于开发人员。 有关适用于 Windows 的 DVD 解码器（包括软件解码器列表）的常规信息，请参阅 Microsoft 支持部门网站上的[windows Media Player 插件和加载项](https://support.microsoft.com/help/17948/plug-ins-and-add-ons-for-windows-media-player)。

Windows 98/Me 和更高版本以及 Windows 2000 及更高版本支持 DVD 解码器。

若要编写 DVD 解码器微型驱动程序，微型驱动程序必须包含 WDK 中提供的*ksmedia*和*ntddcdvd*标头文件。 微型驱动程序还必须链接到*stream .lib*、 *ksguid*、dxapi *ks.lib*库和*dxapi.lib*库。

在 Windows XP 下，以下组件支持 DVD 解码和播放：

- **WDM 流类驱动程序**

    WDM 流类驱动程序支持流数据类型和 MPEG-2 和 AC'97 硬件解码器。 有关详细信息，请参阅[流式处理微型驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)。

    > [!NOTE]
    > Microsoft 不提供与 Windows XP 一起提供的 MPEG-2 或 AC'97 软件/硬件解码器筛选器。 供应商必须为每个所需的 DVD 数据流提供与 DirectShow 兼容的软件解码器，或提供一个与 WDM 流兼容的 DVD 解码器微型驱动程序来支持其 DVD 硬件解码器。

- **DVD-ROM 类驱动程序**

    Windows XP 中通过更新的 CD-ROM 类驱动程序提供了对 DVD-ROM 命令集的支持，包括用于版权保护和实行的命令。 此类驱动程序提供从 DVD-ROM 驱动器读取数据扇区的功能。

- **UDF 文件系统**

    基于 NT 的操作系统提供 UDF 可安装的文件系统，类似于 FAT 和 NTFS。 此可安装文件系统支持 UDF 格式的 DVD 光盘。

- Microsoft **DirectShow**

  DirectShow 筛选器和相关支持包括 DVD 导航器/拆分器、用于与硬件解码器微型驱动程序（用于视频）、子画面和音频流、line21 解码器（隐藏式字幕）、视频混合器、视频呈现器和音频呈现器的代理筛选器。

  - DirectShow DVD 导航器/拆分器筛选器

    DVD 导航器/拆分器筛选器解释嵌入在 DVD 影片中的编程语言、家长控制和多种语言，并处理大多数特定于 DVD 的数据结构。 此筛选器直接从 DVD 光盘读取 DVD 流，并生成单独的媒体类型输出，如音频、视频和子画面。 筛选器将响应流中的命令并处理所有用户输入。

  - DirectShow 代理筛选器

    此筛选器将 DirectShow 接口转换为 WDM 连接和流体系结构属性。 它为每个要解码的数据类型（如音频和视频数据类型）创建（即实例化）每个数据类型的设备对象。 此筛选器支持允许扩展新接口的插件。

  - DirectShow 关闭标题解码筛选器

    此筛选器将 DVD 视频流中的隐藏式字幕数据转换为文本图像。

  - DirectShow 视频端口管理器和呈现筛选器

    这些筛选器允许使用硬件视频端口播放视频，并支持混合低带宽视频流，如隐藏式字幕解码器输出流。

- Microsoft **DIRECTDRAW HAL 和 VPE**

专用总线将已解码的视频流从 MPEG-2 解码器传输到显示卡。 Microsoft 通过使用具有视频端口扩展（VPE）的 DirectDraw 硬件抽象层（HAL）将在硬件中解码的视频传递到视频图形阵列（VGA），为这些接口提供软件支持。 对于软件解码器，可以使用加速图形端口（AGP）总线将解码视频传输到 VGA。

- **版权保护**

    适用于 DVD 的版权保护是通过加密光盘上的扇区来提供的，然后在解码这些扇区之前对其进行解密。 Microsoft 通过使用 DVD 导航器/拆分器来支持软件和硬件 decrypters，该方法监督计算机上的解码器和 DVD-ROM 驱动器之间的身份验证顺序。 密钥交换序列通过发送到 DVD 解码器微型驱动程序的输入插针的属性实现。

DVD 播放有两种主要形式：

[基于硬件的 DVD 解码](hardware-based-dvd-decoding.md)

[基于软件的 DVD 解码](software-based-dvd-decoding.md)

以下主题概述了与 DVD 解码器相关的内核流式处理属性和事件：

[与 DVD 解码器相关的 KS 属性](dvd-decoder-related-ks-properties.md)

[与 DVD 解码器相关的 KS 事件](dvd-decoder-related-ks-events.md)
