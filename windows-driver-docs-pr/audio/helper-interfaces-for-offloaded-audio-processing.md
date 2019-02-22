---
title: 卸载音频处理的帮助程序接口
description: 本主题介绍 PortCls 使用帮助程序接口，以简化驱动程序支持卸载音频处理。
ms.assetid: 9C78621E-9824-4992-9D7E-BCF3B51F1BFB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cd0728ed4ad791d1b3411c90139861e53d71b24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555167"
---
# <a name="helper-interfaces-for-offloaded-audio-processing"></a>卸载音频处理的帮助程序接口


本主题介绍了 Microsoft 已添加到其音频端口类驱动程序 (PortCls)，以简化驱动程序实现的帮助程序接口，支持卸载音频处理。

当您的 WaveRT 微型端口驱动程序适用于能够处理硬件卸载音频流的音频适配器的开发时，微型端口驱动程序适用于 PortCls 流和/或进程的音频数据。

已更新 PortCls 来处理所有卸载相关内核流式处理 (KS) 属性，并且这是什么可以轻松地开发 WaveRT 微型端口驱动程序，以公开对处理硬件卸载音频流的支持。 由于更新而 PortCls 仅调用基础微型端口驱动程序硬件和/或通过两个新定义的接口的特定于驱动程序的操作：

-   [**IMiniportAudioEngineNode**](https://msdn.microsoft.com/library/windows/hardware/dn302040)

-   [**IMiniportStreamAudioEngineNode**](https://msdn.microsoft.com/library/windows/hardware/dn265090)

您必须开发两个类可以使用这些接口，一个用于每个接口。

## <a name="span-idworkingwithiminiportaudioenginenodespanspan-idworkingwithiminiportaudioenginenodespanspan-idworkingwithiminiportaudioenginenodespanworking-with-iminiportaudioenginenode"></a><span id="Working_with_IMiniportAudioEngineNode"></span><span id="working_with_iminiportaudioenginenode"></span><span id="WORKING_WITH_IMINIPORTAUDIOENGINENODE"></span>使用 IMiniportAudioEngineNode


开发要使用的类**IMiniportAudioEngineNode**，还必须继承自[IMiniportWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536737)。 中定义的方法**IMiniportAudioEngineNode**允许驱动程序以使用用于访问音频引擎通过 KS 筛选器句柄的 KS 属性。 类/接口层次结构如下所示：

![自定义 wavert 微型端口类继承从 iminiportwavert 和 iminiportaudioenginenode。](images/offload-class-hier1.png)

因此如果，例如，您开发一个名为 CYourMiniportWaveRT 类，然后从上图中，您可以看到 CYourMiniportWaveRT 必须实现定义的所有方法 （显示为操作） 适用于两个父接口。

这样的类的主干模板将包含以下代码：

```ManagedCPlusPlus
class CMiniportWaveRT : 
    public IMiniportWaveRT,
    public IMiniportAudioEngineNode,
    public CUnknown
{
...

    IMP_IMiniportWaveRT;
    IMP_IMiniportAudioEngineNode;
...

};
```

*Portcls.h*标头文件定义了这些接口。

## <a name="span-idworkingwithiminiportstreamaudioenginenodespanspan-idworkingwithiminiportstreamaudioenginenodespanspan-idworkingwithiminiportstreamaudioenginenodespanworking-with-iminiportstreamaudioenginenode"></a><span id="Working_with_IMiniportStreamAudioEngineNode"></span><span id="working_with_iminiportstreamaudioenginenode"></span><span id="WORKING_WITH_IMINIPORTSTREAMAUDIOENGINENODE"></span>使用 IMiniportStreamAudioEngineNode


开发并将其与第二个接口，协同工作的类**IMiniportStreamAudioEngineNode**，还必须继承自[IMiniportWaveRTStreamNotification](https://msdn.microsoft.com/library/windows/hardware/ff536739)。 中定义的方法**IMiniportStreamAudioEngineNode**允许驱动程序以使用 KS 属性的访问通过 pin 实例句柄的音频引擎。 类/接口层次结构如下所示：

![自定义 wavert 流微型端口类继承从 iminiportwavertstreamnotification 和 iminiportstreamaudioenginenode。](images/offload-class-hier2.png)

因此如果，例如，您开发一个名为 CYourMiniportWaveRTStream 类，然后从上图中，您可以看到 CYourMiniportWaveRTStream 必须实现适用于两个父接口定义的所有方法。

这样的类的主干模板将包含以下代码：

```ManagedCPlusPlus
class CMiniportWaveRTStream : 
    public IMiniportWaveRTStreamNotification,
    public IMiniportStreamAudioEngineNode,
    public CUnknown
{
...
    IMP_IMiniportWaveRTStream;
    IMP_IMiniportWaveRTStreamNotification;
    IMP_IMiniportStreamAudioEngineNode;
...

};
```

*Portcls.h*标头文件定义了这些接口。 有关如何开发驱动程序可以处理硬件卸载音频流的详细信息，请参阅[驱动程序实现细节](driver-implementation-details.md)。

 

 




