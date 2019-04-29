---
title: AVStream 中的硬件编解码器支持
description: AVStream 中的硬件编解码器支持
ms.assetid: 19ffd906-e198-4ede-b132-45e53431603c
keywords:
- AVStream WDK，硬件编解码器支持
- 硬件编解码器支持 WDK AVStream
- AVStream 硬件编解码器支持 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7908decf3f5e5355277d3e27eac4fd0f1011cf4e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363601"
---
# <a name="hardware-codec-support-in-avstream"></a>AVStream 中的硬件编解码器支持


在 Windows 7 和更高版本的 Windows 中，基于 AVStream 的媒体设备可以显示为用户模式应用程序的媒体基础转换 (MFT) 筛选器。

此功能，作为用户模式下媒体基础转换 (Mft) 提供基于硬件的解码器和编码器，视频处理器的硬件供应商。

基于硬件的编码和解码极大地改善了用户体验。

若要启用在 AVStream 硬件编解码器支持，供应商提供基于 AVStream 的微型驱动程序公开解码、 编码和视频处理时，分别作为单独的 AVStream 筛选器。 然后，操作系统会创建用户模式下 MFT 对应于每个 AVStream 筛选器。 用户模式应用程序然后可以通过使用 IMFTransform 接口函数中定义的提交代码转换请求到 Mft [Media Foundation SDK](https://go.microsoft.com/fwlink/p/?linkid=144771)。

本部分介绍所需的 AVStream 驱动程序以使用此功能的更改。

本部分包含以下主题：

[开始使用硬件中 AVStream 编解码器支持](getting-started-with-hardware-codec-support-in-avstream.md)

[处理数据类型协商中 AVStream 编解码器](handling-data-type-negotiation-in-avstream-codecs.md)

[使用硬件媒介中 AVStream 编解码器](using-hardware-mediums-in-avstream-codecs.md)

[指定分配器组帧中 AVStream 编解码器](specifying-allocator-framing-in-avstream-codecs.md)

[描述 AVStream 编解码器中的扩展的示例信息](describing-extended-sample-information-in-avstream-codecs.md)

[在 AVStream 编解码器支持动态格式更改](supporting-dynamic-format-changes-in-avstream-codecs.md)

[处理 AVStream 编解码器中的 Stream 的末尾](handling-end-of-stream-in-avstream-codecs.md)

[重置 AVStream 编解码器中的状态](resetting-state-in-avstream-codecs.md)

[处理在 AVStream 编解码器](handling-stride-in-avstream-codecs.md)

[安装 AVStream 基于硬件的编解码器驱动程序](installing-an-avstream-based-hardware-codec-driver.md)

 

 




