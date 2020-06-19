---
title: AVStream 中的硬件编解码器支持
description: AVStream 中的硬件编解码器支持
ms.assetid: 19ffd906-e198-4ede-b132-45e53431603c
keywords:
- AVStream WDK，硬件编解码器支持
- 硬件编解码器支持 WDK AVStream
- AVStream 硬件编解码器支持 WDK
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 04c941ec153dc6ba61afe477c26c25d2b99e0b4a
ms.sourcegitcommit: 8143bb312ead6582b4b3e0ad34b6266dcfd74fb5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "84992475"
---
# <a name="hardware-codec-support-in-avstream"></a>AVStream 中的硬件编解码器支持

基于 AVStream 的媒体设备可以显示为用户模式应用程序媒体基础转换（MFT）筛选器。

此功能允许硬件供应商以用户模式媒体基础转换（MFTs）的形式提供基于硬件的解码器、编码器和视频处理器。

基于硬件的编码和解码极大地提高了用户体验。

为了在 AVStream 中启用硬件编解码器支持，供应商提供了一种基于 AVStream 的微型驱动程序，其中每个都是单独的 AVStream 筛选器。 然后，操作系统会创建对应于每个 AVStream 筛选器的用户模式 MFT。 然后，用户模式应用程序可以通过使用[媒体基础 SDK](https://docs.microsoft.com/windows/win32/medfound/microsoft-media-foundation-sdk)中定义的 IMFTransform 接口函数，将转码请求提交到 MFTs。

本部分介绍 AVStream 驱动程序使用此功能所需的更改。

本节包含下列主题：

[AVStream 中的硬件编解码器支持入门](getting-started-with-hardware-codec-support-in-avstream.md)

[在 AVStream 编解码器中处理数据类型协商](handling-data-type-negotiation-in-avstream-codecs.md)

[在 AVStream 编解码器中使用硬件媒体](using-hardware-mediums-in-avstream-codecs.md)

[在 AVStream 编解码器中指定分配器组帧](specifying-allocator-framing-in-avstream-codecs.md)

[描述 AVStream 编解码器中的扩展示例信息](describing-extended-sample-information-in-avstream-codecs.md)

[在 AVStream 编解码器中支持动态格式更改](supporting-dynamic-format-changes-in-avstream-codecs.md)

[处理 AVStream 编解码器中的流结尾](handling-end-of-stream-in-avstream-codecs.md)

[重置 AVStream 编解码器中的状态](resetting-state-in-avstream-codecs.md)

[处理 AVStream 编解码器中的步幅](handling-stride-in-avstream-codecs.md)

[安装基于 AVStream 的硬件编解码器驱动程序](installing-an-avstream-based-hardware-codec-driver.md)
