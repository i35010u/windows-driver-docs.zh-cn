---
title: 处理 AVStream 编解码器中的流结尾
description: 处理 AVStream 编解码器中的流结尾
ms.assetid: ee57137b-999a-449f-9f9d-50bc19e07ba8
keywords:
- 处理流 WDK AVStream 结尾
- WDK AVStream 流的末尾
- 硬件编解码器支持 WDK AVStream，流的末尾
- AVStream 硬件编解码器支持 WDK、 处理流的末尾
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f071e544d1e623798d63402a4e6395b0b048e7bb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384038"
---
# <a name="handling-end-of-stream-in-avstream-codecs"></a>处理 AVStream 编解码器中的流结尾


当 HW MFT 接收端流 (EOS) 标志设置的示例时，它会设置 KSSTREAM\_标头\_OPTIONSF\_中的 ENDOFSTREAM **OptionsFlag**隶属[ **KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)结构，它对应于该示例。

微型驱动程序收到后[ **KSSTREAM\_指针**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksstream_pointer)与 KSSTREAM\_标头\_OPTIONSF\_ENDOFSTREAM 标志中设置**StreamHeader.OptionsFlag**，输入插针将不会收到任何新输入的流指针，直到微型驱动程序设置 KSSTREAM\_标头\_OPTIONSF\_ENDOFSTREAM 上输出流指针。

微型驱动程序设置 KSSTREAM 之前\_标头\_OPTIONSF\_ENDOFSTREAM 上输出流指针，它应生成尽可能使用当前可用的输入输出的帧数。

微型驱动程序应则清除任何缓存与以前处理过流指针，除了与这些流指针关联的数据相关的信息。 然后微型驱动程序应设置 KSSTREAM\_标头\_OPTIONSF\_ENDOFSTREAM 的输出插针。

微型驱动程序应将到达的新输入的流指针随后作为新流的一部分。 例外情况是如果 EOS 时，会出现的媒体流中断。 如果是这样，新到达流指针必须 KSSTREAM\_标头\_OPTIONSF\_DATADISCONTINUITY 或 KSSTREAM\_标头\_OPTIONSF\_TIMEDISCONTINUITY，或KSSTREAM 中设置两个，标志\_标头。**OptionsFlags**。 如果流指针，这些标志集之一到达输入插针，微型驱动程序必须在相应输出插针流指针上设置相同的标记。

 

 




