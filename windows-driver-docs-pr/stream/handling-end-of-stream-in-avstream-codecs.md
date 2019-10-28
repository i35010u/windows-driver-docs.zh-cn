---
title: 处理 AVStream 编解码器中的流结尾
description: 处理 AVStream 编解码器中的流结尾
ms.assetid: ee57137b-999a-449f-9f9d-50bc19e07ba8
keywords:
- 处理流终止 WDK AVStream
- 流终止 WDK AVStream
- 硬件编解码器支持 WDK AVStream，流结束
- AVStream 硬件编解码器支持 WDK，处理流的结尾
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c98259e9d7399fe611cca46ffb59bfc800bb814
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838088"
---
# <a name="handling-end-of-stream-in-avstream-codecs"></a>处理 AVStream 编解码器中的流结尾


当 HW MFT 接收到带有流（EOS）标记结尾的示例时，它将在与该示例相对应的[**KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)结构的**OptionsFlag**成员中设置 KSSTREAM\_标头\_OPTIONSF\_ENDOFSTREAM.

在微型驱动程序收到包含 KSSTREAM\_标头的[**KSSTREAM\_指针**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksstream_pointer)\_OPTIONSF 在**ENDOFSTREAM**中设置\_StreamHeader 标志后，在微型驱动程序在输出流指针上将 KSSTREAM\_标头设置\_OPTIONSF\_ENDOFSTREAM。

在输出流指针上微型驱动程序设置 KSSTREAM\_标头\_OPTIONSF\_ENDOFSTREAM 之前，它应使用当前可用的输入生成尽可能多的输出帧。

然后，微型驱动程序应清除与以前处理的流指针相关的任何缓存信息，以及与这些流指针关联的数据。 然后，微型驱动程序应在输出插针上设置 KSSTREAM\_标头\_OPTIONSF\_ENDOFSTREAM。

微型驱动程序应将随后到达的新输入流指针视为新流的一部分。 例外情况是由于媒体流中的不连续性导致的 EOS。 如果是这种情况，则新到达的流指针将具有 KSSTREAM\_标头\_OPTIONSF\_DATADISCONTINUITY 或 KSSTREAM\_标头\_OPTIONSF\_TIMEDISCONTINUITY，或者两者都是 KSSTREAM 中的标志集\_标头.**OptionsFlags**。 如果具有其中一个标志集的流指针到达输入插针，则微型驱动程序必须在相应的输出插针的流指针上设置相同的标志。

 

 




