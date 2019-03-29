---
title: METransformNeedInput
description: METransformNeedInput 事件指示设备转换需要一个输入。
ms.assetid: AACD80F6-90A1-4338-AE5B-4A9248747949
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d40168ae5fd48a8e5da49aa04aefbdabfd3cb24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568733"
---
# <a name="metransformneedinput"></a>METransformNeedInput


**METransformNeedInput**事件指示设备转换需要一个输入。

## <a name="span-idwhensentspanspan-idwhensentspanspan-idwhensentspanwhen-sent"></a><span id="When_sent"></span><span id="when_sent"></span><span id="WHEN_SENT"></span>发送时


当设备转换需要输入生成的输出时发送此事件。 通常情况下，异步 Mft 使用此消息可获取输入的示例进行处理并生成一个输出示例。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


| 参数              | 描述                                                                                                   |
|------------------------|---------------------------------------------------------------------------------------------------------------|
| **输入的流索引** | 作为 IMFMediaEvent 属性存储中发送的输入的流索引**MF\_事件\_MFT\_输入\_流\_ID**。 |

 

## <a name="remarks"></a>备注


此事件将不处理设备转换管理器 (DTM) 由于以下原因：

-   Devproxy 不具有任何输入插针
-   即使设备 MFT 具有输入插针，它是 Devproxy 输出可用时自动送入示例。 因此，没有需要设备 MFT 请求的示例。 DTM 会忽略此请求。

 

 





