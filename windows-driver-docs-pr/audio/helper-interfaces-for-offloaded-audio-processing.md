---
title: 用于已卸载音频的处理的帮助程序接口
description: 本主题介绍了 PortCls helper 接口，以简化支持卸载音频处理的驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 252c8d45e9f7e12f76de9396290f491281b1ce85
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789197"
---
# <a name="helper-interfaces-for-offloaded-audio-processing"></a>用于已卸载音频的处理的帮助程序接口


本主题介绍 Microsoft 在 PortCls) 中添加到其音频端口级驱动 (程序的帮助器接口，以简化支持卸载音频处理的驱动程序的实现。

当你开发的 WaveRT 微型端口驱动程序将适用于能够处理硬件卸载音频流的音频适配器时，微型端口驱动程序可与 PortCls 配合使用来流式传输和/或处理音频数据。

PortCls 已更新为处理所有与卸载相关的内核流式处理 (KS) 属性，这就使得开发 WaveRT 微型端口驱动程序以公开对处理硬件卸载音频流的支持变得简单。 作为更新的结果，PortCls 仅通过两个新定义的接口为硬件和/或驱动程序特定的操作调用基础微型端口驱动程序：

-   [**IMiniportAudioEngineNode**](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportaudioenginenode)

-   [**IMiniportStreamAudioEngineNode**](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportstreamaudioenginenode)

必须开发两个类，才能使用这些接口，每个接口各有一个。

## <a name="span-idworking_with_iminiportaudioenginenodespanspan-idworking_with_iminiportaudioenginenodespanspan-idworking_with_iminiportaudioenginenodespanworking-with-iminiportaudioenginenode"></a><span id="Working_with_IMiniportAudioEngineNode"></span><span id="working_with_iminiportaudioenginenode"></span><span id="WORKING_WITH_IMINIPORTAUDIOENGINENODE"></span>使用 IMiniportAudioEngineNode


开发用于 **IMiniportAudioEngineNode** 的类还必须从 [IMiniportWaveRT](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert)继承。 **IMiniportAudioEngineNode** 中定义的方法允许您的驱动程序使用通过 ks 筛选器句柄访问音频引擎的 KS 属性。 类/接口层次结构如下所示：

![自定义 wavert 微型端口类继承自 iminiportwavert 和 iminiportaudioenginenode。](images/offload-class-hier1.png)

例如，如果你开发一个名为 CYourMiniportWaveRT 的类，然后从前面的关系图中可以看到，则 CYourMiniportWaveRT 必须实现 (显示为两个父接口) 定义的操作的所有方法。

此类类的框架模板将包含以下代码：

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

*Portcls* 头文件定义这些接口。

## <a name="span-idworking_with_iminiportstreamaudioenginenodespanspan-idworking_with_iminiportstreamaudioenginenodespanspan-idworking_with_iminiportstreamaudioenginenodespanworking-with-iminiportstreamaudioenginenode"></a><span id="Working_with_IMiniportStreamAudioEngineNode"></span><span id="working_with_iminiportstreamaudioenginenode"></span><span id="WORKING_WITH_IMINIPORTSTREAMAUDIOENGINENODE"></span>使用 IMiniportStreamAudioEngineNode


你开发的用于处理第二个接口（ **IMiniportStreamAudioEngineNode**）的类还必须从 [IMiniportWaveRTStreamNotification](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstreamnotification)继承。 **IMiniportStreamAudioEngineNode** 中定义的方法允许您的驱动程序使用通过 pin 实例句柄访问音频引擎的 KS 属性。 类/接口层次结构如下所示：

![自定义的 wavert 流微型端口类继承自 iminiportwavertstreamnotification 和 iminiportstreamaudioenginenode。](images/offload-class-hier2.png)

例如，如果您开发一个名为 CYourMiniportWaveRTStream 的类，然后从前面的关系图中可以看到，则 CYourMiniportWaveRTStream 必须实现为这两个父接口定义的所有方法。

此类类的框架模板将包含以下代码：

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

*Portcls* 头文件定义这些接口。 有关如何开发可处理硬件卸载音频流的驱动程序的详细信息，请参阅 [驱动程序实现细节](driver-implementation-details.md)。

 

