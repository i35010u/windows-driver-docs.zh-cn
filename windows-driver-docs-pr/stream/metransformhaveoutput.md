---
title: METransformHaveOutput
description: METransformHaveOutput 事件指示设备转换一个其输出流上有准备一个示例。
ms.assetid: 1CD11A3C-8181-4AF2-9AB3-10B04668CF1C
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb4e197292db24f0c882d80b8e5834a49b23ec2c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353685"
---
# <a name="metransformhaveoutput"></a>METransformHaveOutput


**METransformHaveOutput**事件指示设备转换具有一个其输出流上准备一个示例。

## <a name="span-idwhensentspanspan-idwhensentspanspan-idwhensentspanwhen-sent"></a><span id="When_sent"></span><span id="when_sent"></span><span id="WHEN_SENT"></span>发送时


Devproxy 或设备 MFT 引发此事件时它们准备好的示例对其输出流，以拾取设备转换管理器 (DTM)。

当 Devproxy 引发 METransformHaveOutput 时，DTM 会对 Devproxy 调用 ProcessOutput。 生成的示例将送入设备 MFT 相应的输入。

当引发设备 MFT **METransformHaveOutput**，DTM 将中继到设备源的事件。 设备源会对设备转换管理器将被传送至设备 MFT 调用过程的输出。 因此该示例会将拾取设备源，应输入媒体管道。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


无。

## <a name="remarks"></a>备注


设备 MFT 将接收的总输出流计数**MFT\_输出\_数据\_缓冲区**中数组的结构。 它需要填写具有适当的值的结构成员。 之前返回到设备 MFT DTM 调用来检索的示例，以响应**METransformHaveOutput**消息，另一个示例变得可供另一个流，如果设备 MFT 将继续操作并在此发送示例ProcessOutput 调用。 DTM 将 ProcessOutput 再次调用，但在该时间，设备 MFT 可以只返回与没有样本调用如果全都不可用。

有关详细信息，请参阅[ **IMFDeviceTransform::ProcessOutput**](https://msdn.microsoft.com/library/windows/hardware/mt797682)。

 

 





