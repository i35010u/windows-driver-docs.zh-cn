---
title: 格式协商
description: 格式协商
ms.assetid: 5b6ee5ed-de5a-4832-a581-179966e79dbd
ms.date: 11/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: d02eedae2c98dcd7b2f46093ed87b2fd20c4c34c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543454"
---
# <a name="format-negotiation"></a>格式协商


应用程序启动音频处理后，图形生成器 sAPOs 配置到音频图形，还可以初始化 sAPOs。 与 LFX sAPO 建立音频数据的输入和输出 sAPO 格式然后协商音频服务。 这个协商过程被称为格式协商。

提供适用于 Windows Vista 音频系统效果的所有 sAPOs 必须都具有某些接口和方法。 SAPO 和音频引擎用来协商的数据格式的方法是： **IsInputFormatSupported**方法**IAudioProcessingObject**接口和**LockForProcess**并**UnlockForProcess**的方法**IAudioProcessingObjectConfiguration**接口。 

若要启动格式协商，音频服务将首先为默认值基于 float32 的格式设置 LFX sAPO 的输出。 音频服务然后调用**IAudioProcessingObject::IsInputFormatSupported**方法的 LFX sAPO，建议的默认格式，并监视此方法的 HRESULT 的响应。 如果 LFX sAPO 可以支持的建议的格式，它将返回 S\_确定，以及对受支持的格式的引用。 如果 LFX sAPO 无法支持建议的格式，它将返回 S\_FALSE 以及对建议一个与最接近的格式的引用。 如果 LFX sAPO 不能支持建议的格式，并且没有接近的匹配项，它将返回 APOERR\_格式\_不\_受支持。 GFX sAPO 配合 LFX sAPO 的输出格式。 因此 GFX sAPO 没有包括在格式协商过程中。

数据格式选择用于处理的音频数据后，调用音频处理图形生成器**IAudioProcessingObjectConfiguration::LockForProcess** sAPOs，从而导致完成而格式选择的方法。

如果 Windows Vista sAPO 将错误返回到以响应对的调用包装自定义 sAPO **LockForProcess**方法中，自定义 sAPO 必须处理该错误处理从错误的相同方式**CoCreateInstance**尝试实例化 sAPO 失败时。 Spkrfill.cpp 文件，了解有关如何覆盖系统提供 LockForProcess 方法的详细信息，请参阅。

由于音频服务运行的方式，LFX 和 GFX sAPOs 必须能够互相独立地响应的查询，从有关的数据格式的音频服务。

**重要**  时实现自定义 sAPO 包装 Windows Vista LFX sAPO，请勿指定 APO\_标志\_FRAMESPERSECOND\_必须\_注册中的匹配项标志自定义 sAPO 的属性。 如果指定此标志，Windows Vista LFX sAPO 将不能执行演讲者填充、 耳机虚拟化或虚拟环绕。 此外，自定义 sAPO 将不能混任何音频流。 例如，自定义 sAPO 将不能混用下两个通道立体声音频流的 5.1 音频流。

 

 

 




