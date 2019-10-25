---
title: COM 对象的引用计数约定
description: COM 对象的引用计数约定
ms.assetid: e6b19110-37e2-4d23-a528-6393c12ab650
keywords:
- COM 对象引用 WDK 音频
- 对象引用 WDK 音频
- 统计引用 WDK 音频
- 引用计数 WDK 音频
- 输入参数引用统计 WDK 音频
- 输出参数引用统计 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3e431a2cecc8f9f77c49d96682c1ade172b2d9c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832442"
---
# <a name="reference-counting-conventions-for-com-objects"></a>COM 对象的引用计数约定


## <span id="reference_counting_conventions_for_com_objects"></span><span id="REFERENCE_COUNTING_CONVENTIONS_FOR_COM_OBJECTS"></span>


音频接口中的方法遵循一组常规规则，用于对它们作为输入参数或作为输出参数返回的 COM 对象上的引用进行计数。 下面总结了这些规则及其例外情况。 有关 COM 接口的详细信息，请参阅 Microsoft Windows SDK 文档的 COM 部分。

### <a name="span-idreference_counting_on_input_parametersspanspan-idreference_counting_on_input_parametersspanspan-idreference_counting_on_input_parametersspanreference-counting-on-input-parameters"></a><span id="Reference_Counting_on_Input_Parameters"></span><span id="reference_counting_on_input_parameters"></span><span id="REFERENCE_COUNTING_ON_INPUT_PARAMETERS"></span>输入参数上的引用计数

在调用采用对象*X*引用作为输入参数的方法时，调用方必须在调用的持续时间内保留自己对对象的引用。 此行为是必需的，以确保方法的指针到对象*X*在返回前一直有效。 如果实现此方法的对象*Y*需要在从此方法返回之外保存对对象*x*的引用，则该方法应在返回之前在对象*x*上调用[**AddRef**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref) 。 当对象*Y*在以后使用对象*x*完成时，它应调用对象*x*上的[**Release**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-release) 。

例如， [**IServiceGroup：： AddMember**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicegroup-addmember)方法对其添加到其服务组的[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)对象调用[**AddRef**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref) 。 若要对此行为进行补充， [**IServiceGroup：： RemoveMember**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicegroup-removemember)方法会对从服务组中移除的 IServiceSink 对象调用[**Release**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-release) 。

### <a name="span-idreference_counting_on_output_parametersspanspan-idreference_counting_on_output_parametersspanspan-idreference_counting_on_output_parametersspanreference-counting-on-output-parameters"></a><span id="Reference_Counting_on_Output_Parameters"></span><span id="reference_counting_on_output_parameters"></span><span id="REFERENCE_COUNTING_ON_OUTPUT_PARAMETERS"></span>输出参数上的引用计数

通过 output 参数将对象引用传递给调用方的方法应在返回之前在对象上调用[**AddRef**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref) （或在释放自己对对象的引用之前）。 此行为是必需的，以确保调用方在从调用返回时保存有效引用。 调用方负责在使用完对象后对其调用[**Release**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-release) 。

例如， [**IMiniportWaveCyclic：： newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-newstream)方法对流、服务组和 DMA 通道对象调用[**AddRef**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref) ，并将其输出到调用方（WaveCyclic 端口驱动程序）。 调用方负责在不再需要这些引用时将其释放。 有关显示此行为的**IMiniportWaveCyclic：： newstream.ischecked**方法的实现，请参阅 Microsoft Windows 驱动程序工具包（WDK）中的 Sb16 示例适配器。

### <a name="span-idexceptions_to_the_rulesspanspan-idexceptions_to_the_rulesspanspan-idexceptions_to_the_rulesspanexceptions-to-the-rules"></a><span id="Exceptions_to_the_Rules"></span><span id="exceptions_to_the_rules"></span><span id="EXCEPTIONS_TO_THE_RULES"></span>规则的例外

有关此方法在其*DmaChannel* output 参数上执行的非常规引用计数的说明，请参阅[**IMiniportWavePci：： newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)。

 

 




