---
title: 描述 AVStream 编解码器中的扩展示例信息
description: 描述 AVStream 编解码器中的扩展示例信息
ms.assetid: 04447525-78f5-4c77-9a41-4e6e4729f729
keywords:
- AVStream 硬件编解码器支持 WDK，扩展的示例信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76148fe0ae5617f948b271213e8e87b0c7218552
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374083"
---
# <a name="describing-extended-sample-information-in-avstream-codecs"></a>描述 AVStream 编解码器中的扩展示例信息


解码器筛选器可以在扩展中找到扩展的示例信息[ **KSSTREAM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff567138)结构[ **KS\_帧\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff567645)，后者按照 KSSTREAM\_在内存中的标头。

该驱动程序必须将传播 KSSTREAM 中指定的信息\_标头。从输出 （目标） KS 插针的输入 （源） OptionsFlags。

编码器应包括扩展的示例信息中扩展 KSSTREAM\_标头结构，KS\_帧\_信息。 具体而言，编码器应更新成员**dwFrameFlags**以指示 KS\_视频\_标志\_我\_框架和 KS\_视频\_标志\_P\_帧，按实际情况。

中 KS 指定图面上 stride\_帧\_信息的 lSurfacePitch 成员 (与 union **Reserved1**成员)。 有关 surface stride 的详细信息，请参阅[AVStream 编解码器在处理 Stride](handling-stride-in-avstream-codecs.md)。

 

 




