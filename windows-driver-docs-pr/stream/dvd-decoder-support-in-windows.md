---
title: Windows 中的 DVD 解码器支持
description: Windows 中的 DVD 解码器支持
ms.assetid: 3a77b6d1-6095-4cf8-8cd4-2e6d80d171c8
keywords:
- DVD 解码器微型驱动程序 WDK，Windows 支持
- 解码器微型驱动程序 WDK DVD，Windows 支持
- DVD 解码器微型驱动程序 WDK、 编写
- 解码器微型驱动程序 WDK DVD、 编写
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ec36ac40b60a05a95ad92ad1cb9b8840f1a389b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387168"
---
# <a name="dvd-decoder-support-in-windows"></a>Windows 中的 DVD 解码器支持





**请注意**  本主题适用于开发人员。 有关 Windows 的 DVD 解码器的常规信息，包括一系列软件解码器，请参阅文章 q306331，文件"[支持 Windows Media Player for Windows XP 和 Windows Vista 中的软件 mpeg-2 DVD 解码器](https://go.microsoft.com/fwlink/p/?linkid=3100&ID=306331)，"在 microsoft知识库。

 

在 Windows 98 中支持 DVD 解码器 / 我和更高版本以及 Windows 2000 及更高版本。

若要编写 DVD 解码器微型驱动程序，微型驱动程序必须包括*ksmedia.h*并*ntddcdvd.h* WDK 中提供的标头文件。 微型驱动程序还必须链接到*stream.lib*， *ks.lib*， *ksguid.lib*，以及*dxapi.lib*库。

在 Windows XP 下的以下组件支持 DVD 解码和播放：

-   **WDM Stream 类驱动程序**

    WDM 流类驱动程序支持流式处理的数据类型和 mpeg-2 和 ac-3 硬件解码器。 有关详细信息，请参阅[流式处理微型驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)。

**请注意**   Microsoft 不提供 mpeg-2 或 ac-3 软件/硬件与 Windows XP 的解码器筛选器。 供应商必须提供每个所需的 DVD 数据流、 任一 DirectShow 兼容软件解码器或提供 WDM 流式处理兼容的 DVD 解码器微型驱动程序以支持其 DVD 硬件解码器。

 

-   **DVD ROM 类驱动程序**

    更新的 CD-ROM 类驱动程序通过 Windows XP 提供 DVD ROM 命令集，包括用于版权保护和区域化，命令的支持。 此类驱动程序提供了从 DVD ROM 驱动器读取数据的扇区的能力。

-   **UDF 文件系统**

    基于 NT 的操作系统提供了 UDF 可安装的文件系统，类似于 FAT 和 NTFS。 此可安装的文件系统支持 UDF 格式的 DVD 光盘。

-   Microsoft **DirectShow**

    DirectShow 筛选器和相关的支持包括 DVD 导航器/拆分器，视频、 子画面和音频流、 line21 解码器 （隐藏式字幕）、 视频混音器，视频呈现器和一个音频硬件解码器微型驱动程序与代理进行连接的筛选器呈现器。

    -   DirectShow DVD 导航器拆分器筛选器

        DVD 拆分器导航器/筛选器解释 DVD 电影、 家长控制、 多种语言中嵌入的编程语言，并处理大多数特定于 DVD 的数据结构。 此筛选器直接从 DVD 光盘读取 DVD 流，并生成单个媒体类型输出，如音频、 视频和子画面。 筛选器响应流中的命令并处理所有用户输入。

    -   DirectShow 代理筛选器

        此筛选器将 DirectShow 接口转换为 WDM 连接和流式处理体系结构属性。 它将创建 （即，实例化） 为硬件，例如音频和视频数据类型中解码每个数据类型的设备对象。 此筛选器支持允许扩展的新接口的插件。

    -   DirectShow 解码关闭标题筛选器

        此筛选器将文本图像转换为 DVD 视频流中的隐藏字幕数据。

    -   DirectShow 视频端口管理器和呈现筛选器

        这些筛选器启用使用硬件视频端口的视频播放，并提供支持用于混合低带宽的视频流，如隐藏式字幕解码器输出流。

-   Microsoft **VPE 使用 DirectDraw HAL**

专用的总线从 mpeg-2 解码器已解码的视频流传输到显示卡。 Microsoft 提供软件支持这些接口使用 DirectDraw 硬件抽象层 (HAL) 的视频端口扩展名 (VPE) 要传递到视频图形数组 (VGA) 的硬件中已解码的视频。 对于软件解码器，加速的图形端口 (AGP) 总线可以用于将解码后的视频传输到 VGA。

-   **版权保护**

    对于 DVD 版权保护提供的加密一张光盘上的扇区和解码它们之前然后解密这些扇区。 Microsoft 支持通过 DVD 导航器/拆分器，其可监视解码器之间的身份验证序列的软件和硬件 decrypters 和 DVD ROM 驱动器在计算机中。 密钥交换序列是通过属性发送到 DVD 解码器微型驱动程序的输入插针实现的。

有两种主要形式的 DVD 播放：

[基于硬件的 DVD 解码](hardware-based-dvd-decoding.md)

[基于软件的 DVD 解码](software-based-dvd-decoding.md)

以下主题汇总了 DVD 解码器相关的内核流式处理属性和事件：

[DVD 解码器相关 KS 属性](dvd-decoder-related-ks-properties.md)

[DVD 解码器相关 KS 事件](dvd-decoder-related-ks-events.md)

 

 




