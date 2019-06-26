---
title: COM 对象的引用计数约定
description: COM 对象的引用计数约定
ms.assetid: e6b19110-37e2-4d23-a528-6393c12ab650
keywords:
- COM 对象的引用 WDK 音频
- 对象引用 WDK 音频
- 计数引用 WDK 音频
- 引用计数 WDK 音频
- 输入的参数引用计数 WDK 音频
- 输出参数引用计数 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d75ff9b24b96ea6acd2179fe843ff931f9369be1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362527"
---
# <a name="reference-counting-conventions-for-com-objects"></a>COM 对象的引用计数约定


## <span id="reference_counting_conventions_for_com_objects"></span><span id="REFERENCE_COUNTING_CONVENTIONS_FOR_COM_OBJECTS"></span>


中的音频接口方法遵循一组常规规则适用于计数引用 COM 对象，它们将作为输入参数或返回为输出参数。 下面概括了这些规则，其异常。 有关 COM 接口的详细信息，请参阅 Microsoft Windows SDK 文档的 COM 部分。

### <a name="span-idreferencecountingoninputparametersspanspan-idreferencecountingoninputparametersspanspan-idreferencecountingoninputparametersspanreference-counting-on-input-parameters"></a><span id="Reference_Counting_on_Input_Parameters"></span><span id="reference_counting_on_input_parameters"></span><span id="REFERENCE_COUNTING_ON_INPUT_PARAMETERS"></span>输入参数的引用计数

当调用方法将对象引用*X*作为输入参数，调用方必须保留自己的引用的对象上调用的持续时间。 此行为很有必要，以确保该方法的对象指针*X*保持有效，直到其返回。 如果该对象*Y*实现此方法需要保留对对象的引用*X*方法应调用此方法返回时，超出[ **AddRef**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)对象上*X*在返回之前。 对象时*Y*更高版本使用对象完*X*，则应调用[**发布**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)对象上*X*。

例如， [ **IServiceGroup::AddMember** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicegroup-addmember)方法调用[ **AddRef** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)上[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)对象，它将添加到其服务组。 补充了此行为[ **IServiceGroup::RemoveMember** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicegroup-removemember)方法调用[**发布**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)上 IServiceSink 对象它从服务组中删除。

### <a name="span-idreferencecountingonoutputparametersspanspan-idreferencecountingonoutputparametersspanspan-idreferencecountingonoutputparametersspanreference-counting-on-output-parameters"></a><span id="Reference_Counting_on_Output_Parameters"></span><span id="reference_counting_on_output_parameters"></span><span id="REFERENCE_COUNTING_ON_OUTPUT_PARAMETERS"></span>输出参数的引用计数

将传递给调用方通过输出参数的对象引用的方法应调用[ **AddRef** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)对象上之前它将返回 （或它之前释放其自己的对象引用）。 此行为很有必要，以确保调用方持有从调用返回时的有效引用。 调用方负责调用[**发行**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)上使用它完成的对象。

例如， [ **IMiniportWaveCyclic::NewStream** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclic-newstream)方法调用[ **AddRef** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)流、 服务组和 DMA 通道它将输出到调用方 （WaveCyclic 端口驱动程序） 的对象。 调用方负责释放这些引用，当不再需要它们时。 实现**IMiniportWaveCyclic::NewStream**方法，用于显示这种行为，请参阅 Sb16 示例适配器在 Microsoft Windows 驱动程序工具包 (WDK)。

### <a name="span-idexceptionstotherulesspanspan-idexceptionstotherulesspanspan-idexceptionstotherulesspanexceptions-to-the-rules"></a><span id="Exceptions_to_the_Rules"></span><span id="exceptions_to_the_rules"></span><span id="EXCEPTIONS_TO_THE_RULES"></span>规则的例外情况

有关此方法执行上的非常规的引用计数的说明及其*DmaChannel*输出参数，请参阅[ **IMiniportWavePci::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-newstream)。

 

 




