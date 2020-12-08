---
title: 格式协商
description: 格式协商
ms.date: 11/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 201c6795d0512613d2cec9167ac96ed8c141c1d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786539"
---
# <a name="format-negotiation"></a>格式协商


在应用程序启动音频处理后，图形生成器将 sAPOs 配置为音频图形并初始化 sAPOs。 然后，音频服务与 LFX sAPO 协商，以便在 sAPO 的输入和输出中建立音频数据的格式。 此协商过程称为 "格式协商"。

为 Windows Vista 提供音频系统影响的所有 sAPOs 必须具有某些接口和方法。 SAPO 和音频引擎用来协商数据格式的方法包括： **IAudioProcessingObject** 接口的 **IsInputFormatSupported** 方法和 **UnlockForProcess** 接口的 **LockForProcess** 和 **IAudioProcessingObjectConfiguration** 方法。 

若要启动格式协商，音频服务首先将 LFX sAPO 的输出设置为基于 float32 的默认格式。 然后，音频服务调用 LFX sAPO 的 **IAudioProcessingObject：： IsInputFormatSupported** 方法，建议默认格式，并监视此方法的 HRESULT 响应。 如果 LFX sAPO 可以支持建议的格式，它将返回 S \_ OK，同时返回对支持的格式的引用。 如果 LFX sAPO 不支持所建议的格式，它将返回 S \_ FALSE，同时返回一个与建议的最匹配的格式的引用。 如果 LFX sAPO 不支持建议的格式，并且没有接近的匹配项，则它将返回 APOERR \_ 格式（ \_ 不 \_ 受支持）。 GFX sAPO 与 LFX sAPO 的输出格式一起工作。 因此，GFX sAPO 不涉及格式协商过程。

选择用于处理音频数据的数据格式后，音频处理图形生成器将调用 sAPOs 的 **IAudioProcessingObjectConfiguration：： LockForProcess** 方法，从而使格式选择完成。

如果 Windows Vista sAPO 在对 **LockForProcess** 方法的调用时向包装自定义 sAPO 返回错误，则自定义 sAPO 必须处理错误，方法是在尝试实例化 sAPO 失败时处理来自 **CoCreateInstance** 的错误。 有关如何覆盖系统提供的 LockForProcess 方法的详细信息，请参阅 Spkrfill 文件。

由于音频服务的运行方式，LFX 和 GFX sAPOs 必须能够彼此独立地做出响应，以便与有关数据格式的音频服务进行查询。

**重要提示**   实现包装 Windows Vista LFX sAPO 的自定义 sAPO 时，请不要 \_ \_ \_ \_ 在自定义 FRAMESPERSECOND 的注册属性中指定 APO 标志 sAPO 必须匹配标志。 如果指定此标志，Windows Vista LFX sAPO 将无法执行演讲者填充、耳机虚拟化或虚拟环绕。 此外，自定义 sAPO 将无法对任何音频流进行关闭。 例如，你的自定义 sAPO 将不能将5.1 音频流混合到两通道立体声音频流中。

 

 

 




