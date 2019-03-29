---
title: METransformFlushInputStream event
description: METransformFlushInputStream 事件通知设备 Transform Manager 刷新已连接到的输入设备 MFT devproxy 的输出流。
ms.assetid: 400FB4BE-90F2-4FF2-A709-7E213D99DCC8
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bb03fc58935a0788ec818b85311c6e215f455ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564025"
---
# <a name="metransformflushinputstream-event"></a>METransformFlushInputStream event


**METransformFlushInputStream**事件通知设备 Transform Manager 刷新已连接到的输入设备 MFT devproxy 的输出流。

这必需的设备 MFT 特定的输出获取刷新时，设备 MFT 的相应输入和连接的 devproxy 流需要刷新。

## <a name="span-idwhensentspanspan-idwhensentspanspan-idwhensentspanwhen-sent"></a><span id="When_sent"></span><span id="when_sent"></span><span id="WHEN_SENT"></span>发送时


当设备 MFT 输出是更改或刷新时，相关的输入的流可能需要刷新。 在这种情况时，设备 MFT 生成此事件。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


| 参数              | 描述                                                                     |
|------------------------|---------------------------------------------------------------------------------|
| **输入的流索引** | 必须上 IMFMediaEvent 属性存储设置的输入的流索引。 |

 

## <a name="remarks"></a>备注


当设备 MFT 输入的流连接的流需要刷新时，它会生成此事件。 在响应此事件时，会调用 DTM [ **FlushOutputStream** ](https://msdn.microsoft.com/library/windows/hardware/mt797665) Devproxy 和它的连接的流将调用[ **FlushInputStream** ](https://msdn.microsoft.com/library/windows/hardware/mt797664) MFT 在设备上。 设备 MFT 将刷新其输入的流，并刷新操作即视为完成。

一般情况下，当将流本身处于运行状态，或者即将停止时，会调用此事件。

 

 





