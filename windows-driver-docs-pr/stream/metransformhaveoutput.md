---
title: METransformHaveOutput
description: METransformHaveOutput 事件表示设备转换在其某个输出流上有一个就绪的示例。
ms.assetid: 1CD11A3C-8181-4AF2-9AB3-10B04668CF1C
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeabd12b66fa5e9a84bd95470ee24caeb047d2dc
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802692"
---
# <a name="metransformhaveoutput"></a>METransformHaveOutput


**METransformHaveOutput**事件表示设备转换在其某个输出流上有一个就绪的示例。

## <a name="span-idwhen_sentspanspan-idwhen_sentspanspan-idwhen_sentspanwhen-sent"></a><span id="When_sent"></span><span id="when_sent"></span><span id="WHEN_SENT"></span>发送时间


当设备转换管理器 (DTM) 在其输出流上准备就绪时，Devproxy 或设备 MFT 会引发此事件。

当 Devproxy 引发 METransformHaveOutput 时，DTM 会调用 ProcessOutput 上的 Devproxy。 生成的示例会送入设备 MFT 的相应输入。

当设备 MFT 引发 **METransformHaveOutput**时，DTM 会将事件中继到设备源。 设备源将在设备转换管理器上调用进程输出，此操作将路由到设备 MFT。 因此，该示例将由设备源选取，并将进入媒体管道。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


无。

## <a name="remarks"></a>备注


设备 MFT 会接收数组中 **MFT \_ 输出 \_ 数据 \_ 缓冲区** 结构的输出流总数。 它应填充具有适当值的结构成员。 在 DTM 回拨到设备 MFT 以检索示例之前，若要响应 **METransformHaveOutput** 消息，如果另一个示例可用于另一个流，则设备 mft 将继续并发送此 ProcessOutput 调用中的示例。 DTM 将再次调用 ProcessOutput，但此时，如果没有任何样本，设备 MFT 就可能只返回没有样本的调用。

有关详细信息，请参阅 [**IMFDeviceTransform：:P rocessoutput**](https://docs.microsoft.com/windows/win32/api/mftransform/nf-mftransform-imfdevicetransform-processoutput)。

 

 





