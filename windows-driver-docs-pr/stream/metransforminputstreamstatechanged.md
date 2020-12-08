---
title: METransformInputStreamStateChanged
description: METransformInputStreamStateChanged 事件表示必须更改输入流状态或媒体类型。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 671fd0103ee9bcff172f4952574d757c99b52aec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840525"
---
# <a name="metransforminputstreamstatechanged"></a>METransformInputStreamStateChanged


**METransformInputStreamStateChanged** 事件表示必须更改输入流状态或媒体类型。

## <a name="span-idwhen_sentspanspan-idwhen_sentspanspan-idwhen_sentspanwhen-sent"></a><span id="When_sent"></span><span id="when_sent"></span><span id="WHEN_SENT"></span>发送时间


更改设备 MFT 输出时，可能还需要更改相关的输入流状态。 出现这种情况时，设备 MFT 会生成一个 **METransformInputStreamStateChanged** 事件。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


| 参数              | 描述                                                                     |
|------------------------|---------------------------------------------------------------------------------|
| **输入流索引** | 必须在 IMFMediaEvent 的属性存储上设置输入流索引。 |

 

## <a name="remarks"></a>备注


对于此事件，设备转换管理器 (DTM) 将在具有指定输入流索引的设备 MFT 上调用 [**GetInputStreamPreferredState**](/windows/win32/api/mftransform/nf-mftransform-imfdevicetransform-getinputstreampreferredstate) 。 设备 MFT 将返回首选的状态和媒体状态。

DTM 会在 devproxy 输出流上设置请求的媒体状态，然后将其转换为请求的流状态。 如果此方法成功，则 DTM 将在设备 MFT 输入流上设置相同的媒体状态，并将其转换为请求的状态。

如果在此过程中出现错误，则 **SetInputStreamStatedwStatus** 参数将包含发生的错误。 设备 MFT 应适当地将错误传播到 DTM。

当指定的流处于停止或运行状态时，可能会生成此事件。 如果流处于停止状态，则设备转换管理器将查询该设备 MFT 输入流的首选类型，并将其设置为 Devproxy 的输出。 如果成功，则 DTM 会在设备 MFT 的输入上设置相同的首选媒体类型。

当设备 MFT 在流式处理时生成此事件时，将停止进一步的示例传递，并将在设备 MFT 输入上请求首选的媒体源。 这种媒体源设置在 Devproxy 的输出和设备 MFT 的输入上设置。 流将在 Devproxy 输出流上自动重新启动，并将示例传递到设备 MFT 输入流。 当新示例到达时，设备 MFT 会将示例传递到相关的输出流。

 

