---
title: 描述 AVStream 编解码器中的扩展示例信息
description: 描述 AVStream 编解码器中的扩展示例信息
ms.assetid: 04447525-78f5-4c77-9a41-4e6e4729f729
keywords:
- AVStream 硬件编解码器支持 WDK，扩展的示例信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87353cffc6772acf60dab9932edc0495d47c0d3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353254"
---
# <a name="describing-extended-sample-information-in-avstream-codecs"></a>描述 AVStream 编解码器中的扩展示例信息


解码器筛选器可以在扩展中找到扩展的示例信息[ **KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)结构[ **KS\_帧\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_frame_info)，后者按照 KSSTREAM\_在内存中的标头。

该驱动程序必须将传播 KSSTREAM 中指定的信息\_标头。从输出 （目标） KS 插针的输入 （源） OptionsFlags。

编码器应包括扩展的示例信息中扩展 KSSTREAM\_标头结构，KS\_帧\_信息。 具体而言，编码器应更新成员**dwFrameFlags**以指示 KS\_视频\_标志\_我\_框架和 KS\_视频\_标志\_P\_帧，按实际情况。

中 KS 指定图面上 stride\_帧\_信息的 lSurfacePitch 成员 (与 union **Reserved1**成员)。 有关 surface stride 的详细信息，请参阅[AVStream 编解码器在处理 Stride](handling-stride-in-avstream-codecs.md)。

 

 




