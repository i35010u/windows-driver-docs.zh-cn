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
ms.openlocfilehash: 9ed8e5cf700158613824ca50a94cf8d66d5f2ec7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190575"
---
# <a name="handling-end-of-stream-in-avstream-codecs"></a>处理 AVStream 编解码器中的流结尾


当 HW MFT 接收到流末尾 (EOS) 标志集的示例时，它将 \_ \_ \_ 在与该示例对应的[**KSSTREAM \_ 标头**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)结构的**OptionsFlag**成员中设置 KSSTREAM 标头 OPTIONSF ENDOFSTREAM。

微型驱动程序接收到[**KSSTREAM \_ 指针**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksstream_pointer)，并在 \_ \_ ENDOFSTREAM 中设置 KSSTREAM 标头 OPTIONSF \_ StreamHeader **StreamHeader.OptionsFlag**标志后，在 OptionsFlag 将微型驱动程序 \_ 标头 \_ KSSTREAM \_ OPTIONSF 设置为输出流指针之前，输入插针不会收到任何新的输入流指针。

在微型驱动程序设置 \_ \_ 输出流指针上的 KSSTREAM 标头 OPTIONSF \_ ENDOFSTREAM 之前，它应使用当前可用的输入生成尽可能多的输出帧。

然后，微型驱动程序应清除与以前处理的流指针相关的任何缓存信息，以及与这些流指针关联的数据。 然后，微型驱动程序应在 \_ \_ 输出插针上设置 KSSTREAM 标头 OPTIONSF \_ ENDOFSTREAM。

微型驱动程序应将随后到达的新输入流指针视为新流的一部分。 例外情况是由于媒体流中的不连续性导致的 EOS。 如果是这种情况，则新到达的流指针将具有 KSSTREAM \_ 标头 \_ OPTIONSF \_ DATADISCONTINUITY 或 KSSTREAM \_ 标头 \_ OPTIONSF \_ TIMEDISCONTINUITY，或同时在 KSSTREAM 标头中设置标志 \_ 。**OptionsFlags**。 如果具有其中一个标志集的流指针到达输入插针，则微型驱动程序必须在相应的输出插针的流指针上设置相同的标志。

 

