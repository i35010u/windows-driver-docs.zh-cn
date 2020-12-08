---
title: METransformNeedInput
description: METransformNeedInput 事件表示设备转换需要输入。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dd5536d93b7403f1af668a42a6a62b6edfd7e79
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832553"
---
# <a name="metransformneedinput"></a>METransformNeedInput


**METransformNeedInput** 事件表示设备转换需要输入。

## <a name="span-idwhen_sentspanspan-idwhen_sentspanspan-idwhen_sentspanwhen-sent"></a><span id="When_sent"></span><span id="when_sent"></span><span id="WHEN_SENT"></span>发送时间


当设备转换需要输入来生成输出时，会发送此事件。 通常，async MFTs 使用此消息获取用于处理和生成输出示例的输入示例。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


| 参数              | 描述                                                                                                   |
|------------------------|---------------------------------------------------------------------------------------------------------------|
| **输入流索引** | 输入流索引作为 **MF \_ 事件 \_ MFT \_ 输入 \_ 流 \_ ID** 发送到 IMFMediaEvent 属性存储中。 |

 

## <a name="remarks"></a>备注


由于以下原因，设备转换管理器不会将此事件处理 (DTM) ：

-   Devproxy 没有任何输入插针
-   即使设备 MFT 有输入插针，它也会在 Devproxy 的输出中提供，自动送入样本。 因此，不需要设备 MFT 来请求示例。 DTM 将忽略此请求。

 

 





