---
title: METransformInputStreamStateChanged
description: METransformInputStreamStateChanged 事件指示输入流状态，或者必须更改媒体类型。
ms.assetid: 734080DD-8D96-4AF3-BB13-FDA8E0398C0B
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0384c0aae1672207c752bc42c5546cc1a8081555
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566221"
---
# <a name="metransforminputstreamstatechanged"></a>METransformInputStreamStateChanged


**METransformInputStreamStateChanged**事件指示输入流状态，或者必须更改媒体类型。

## <a name="span-idwhensentspanspan-idwhensentspanspan-idwhensentspanwhen-sent"></a><span id="When_sent"></span><span id="when_sent"></span><span id="WHEN_SENT"></span>发送时


更改设备 MFT 输出后，相关的输入的流状态可能还需要进行更改。 出现此情况时，生成设备 MFT **METransformInputStreamStateChanged**事件。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


| 参数              | 描述                                                                     |
|------------------------|---------------------------------------------------------------------------------|
| **输入的流索引** | 必须上 IMFMediaEvent 属性存储设置的输入的流索引。 |

 

## <a name="remarks"></a>备注


在响应此事件，设备转换管理器 (DTM) 将调用[ **GetInputStreamPreferredState** ](https://msdn.microsoft.com/library/windows/hardware/mt797670)上设备 MFT 具有指定的输入的流索引。 设备 MFT 将返回的首选的状态和媒体类型。

DTM 将 devproxy 输出流上设置请求的媒体类型，然后将它转换成请求的流式处理状态。 如果成功，然后 DTM 将设备 MFT 输入流设置相同的媒体类型，并将它转换成请求的状态。

如果在此过程中没有错误，然后**SetInputStreamStatedwStatus**参数将包含所发生的错误。 设备 MFT 应传播到相应 DTM 错误。

指定的流处于已停止或正在运行状态时，可能会生成此事件。 如果流已处于停止状态，设备转换管理器将查询该设备 MFT 输入流的首选的类型，并将其设置到 Devproxy 的输出。 如果此操作成功，DTM 将设备 MFT 的输入设置相同的首选媒体类型。

当设备 MFT 生成此事件流式处理，进一步示例传递将停止，而将输入设备 MFT 上请求首选媒体类型。 Devproxy 输出和输入设备 MFT 上设置此媒体类型。 该流将自动重新启动上 Devproxy 输出流和示例将发送到设备 MFT 输入流。 当新的示例，设备 MFT 会将这些示例传送到相关的输出流。

 

 





