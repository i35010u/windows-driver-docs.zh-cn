---
title: 描述 AVStream 编解码器中的扩展示例信息
description: 描述 AVStream 编解码器中的扩展示例信息
ms.assetid: 04447525-78f5-4c77-9a41-4e6e4729f729
keywords:
- AVStream 硬件编解码器支持 WDK，扩展示例信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17df3e29dead68150a4ae31539355eae380a1b7e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844192"
---
# <a name="describing-extended-sample-information-in-avstream-codecs"></a>描述 AVStream 编解码器中的扩展示例信息


解码器筛选器可以在扩展的 KSSTREAM 中找到扩展的示例信息[ **\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)\_[ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)结构

驱动程序必须传播 KSSTREAM 中指定的信息\_标头。OptionsFlags 从输入（源）到输出（目标） KS 引脚。

编码器应在扩展的 KSSTREAM\_标头结构，KS\_帧\_信息中包含扩展的示例信息。 具体而言，编码器应更新成员**dwFrameFlags** ，以指示 KS\_视频\_标志\_I\_框架和 KS\_视频\_\_\_标志。

在 KS\_帧中指定 Surface 步幅\_INFO 的 lSurfacePitch 成员（与**Reserved1**成员联合）。 有关 surface stride 的详细信息，请参阅[AVStream 编解码器中的处理步幅](handling-stride-in-avstream-codecs.md)。

 

 




