---
title: METransformFlushInputStream 事件
description: METransformFlushInputStream 事件通知设备转换管理器刷新连接到设备 MFT 输入的 devproxy 的输出流。
ms.assetid: 400FB4BE-90F2-4FF2-A709-7E213D99DCC8
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f059db29c4613f130184a1b25ac3c66f3ff6e549
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802701"
---
# <a name="metransformflushinputstream-event"></a>METransformFlushInputStream 事件


**METransformFlushInputStream**事件通知设备转换管理器刷新连接到设备 MFT 输入的 devproxy 的输出流。

当刷新设备 MFT 的特定输出、设备 MFT 的相应输入和连接的 devproxy 流时需要刷新此情况。

## <a name="span-idwhen_sentspanspan-idwhen_sentspanspan-idwhen_sentspanwhen-sent"></a><span id="When_sent"></span><span id="when_sent"></span><span id="WHEN_SENT"></span>发送时间


更改或刷新设备 MFT 的输出时，可能需要刷新相关的输入流。 出现这种情况时，设备 MFT 会生成此事件。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


| 参数              | 说明                                                                     |
|------------------------|---------------------------------------------------------------------------------|
| **输入流索引** | 必须在 IMFMediaEvent 的属性存储上设置输入流索引。 |

 

## <a name="remarks"></a>备注


需要刷新设备 MFT 的输入流的连接流时，会生成此事件。 为响应此事件，DTM 会在连接的 Devproxy 流上调用 [**FlushOutputStream**](https://docs.microsoft.com/windows/win32/api/mftransform/nf-mftransform-imfdevicetransform-flushoutputstream) ，并将在设备 MFT 上调用 [**FlushInputStream**](https://docs.microsoft.com/windows/win32/api/mftransform/nf-mftransform-imfdevicetransform-flushinputstream) 。 设备 MFT 会刷新其输入流，刷新操作将被视为已完成。

通常，当流本身处于正在运行状态或将要停止时，将调用此事件。

 

 





