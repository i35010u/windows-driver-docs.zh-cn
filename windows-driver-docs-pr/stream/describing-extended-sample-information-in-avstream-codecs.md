---
title: 描述 AVStream 编解码器中的扩展示例信息
description: 描述 AVStream 编解码器中的扩展示例信息
ms.assetid: 04447525-78f5-4c77-9a41-4e6e4729f729
keywords:
- AVStream 硬件编解码器支持 WDK，扩展示例信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c3896b87bab2b24e3bb5721a59702e5091e7be9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184165"
---
# <a name="describing-extended-sample-information-in-avstream-codecs"></a>描述 AVStream 编解码器中的扩展示例信息


解码器筛选器可以在扩展的 [**KSSTREAM \_ 标头**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header) 结构 [**KS \_ 框架 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)（在内存中跟随 KSSTREAM \_ 标头）中找到扩展的示例信息。

驱动程序必须传播在 KSSTREAM 标头中指定的信息 \_ 。OptionsFlags 从输入 (源) 输出到 (目标) KS pin。

编码器应在扩展的 KSSTREAM \_ 标头结构（KS 帧信息）中包括扩展的示例信息 \_ \_ 。 具体而言，编码器应更新成员 **dwFrameFlags** ，以指示 KS \_ 视频 \_ 标志 \_ I \_ 帧和 ks \_ 视频 \_ 标志 \_ P \_ 帧（如果适用）。

在 KS \_ 帧信息的 lSurfacePitch 成员中指定 Surface stride， \_ (Union 与 **Reserved1** 成员) 。 有关 surface stride 的详细信息，请参阅 [AVStream 编解码器中的处理步幅](handling-stride-in-avstream-codecs.md)。

 

