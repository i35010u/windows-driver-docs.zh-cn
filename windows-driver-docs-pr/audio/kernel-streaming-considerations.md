---
title: 内核流式处理注意事项
description: 内核流式处理注意事项主题阐明了要求和其他蓝牙与相关的特殊注意事项绕过音频流。
ms.assetid: CFC4ACA0-050D-48E1-AA6A-7649040EBF7A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f867918bbfad43a430fc2b1eca2e6409d0d4899
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576693"
---
# <a name="kernel-streaming-considerations"></a>内核流式处理注意事项


内核流式处理注意事项主题阐明了要求和其他特殊注意事项之外的所有音频驱动程序。 这些是内核流式处理与蓝牙旁路音频流式处理更相关的注意事项。

音频驱动程序应完全支持 WaveRT 端口驱动程序，包括"拉取模式。 有关详细信息，请参阅[简介 WaveRT 端口驱动程序](introducing-the-wavert-port-driver.md)。 并且虽然无需实现同步连接面向 (SCO) 的硬件音频引擎绕过输出中，没有执行此操作没有什么坏处。

格式支持的 Windows 徽标要求包括对蓝牙的异常。

音频驱动程序应支持通过旁带硬件的格式。 这通常是 8 KHz 单声道音频流式处理。

## <a name="span-idtopologyspanspan-idtopologyspanspan-idtopologyspantopology"></a><span id="Topology"></span><span id="topology"></span><span id="TOPOLOGY"></span>拓扑


所有蓝牙免提设备支持这两个捕获和呈现。 因此音频驱动程序应公开流式处理 (KS) 内核免提设备，如以下关系图所示，若要支持这两个拓扑呈现，并捕获。

![显示音频驱动程序公开免提设备才支持呈现和捕获 ks 拓扑关系图。](images/btth-bypass-topology.png)

**请注意**  音频驱动程序开发人员可以选择是否实现有单个筛选器，用于同时捕获，呈现路径，或单独的筛选器。 但是，HFP 设备仅允许单个文件对象上 GUID\_DEVINTERFACE\_蓝牙\_HFP\_SCO\_HCIBYPASS 设备接口。 因此使用两个筛选器的设计需要允许这两个筛选器共享的单个文件对象。

 

DAC 和 ADC 节点表示的模拟/数字转换，但不是支持任何 KS 属性。

卷节点支持[ **KSPROPERTY\_音频\_VOLUMELEVEL** ](https://msdn.microsoft.com/library/windows/hardware/ff537309)并[ **KSEVENT\_控件\_更改** ](https://msdn.microsoft.com/library/windows/hardware/ff537128)通过将 SETVOLUME 和 GETVOLUMESTATUSUPDATE Ioctl 发送到 HFP 驱动程序。

卷节点应实现，如下所示：

-   如果将蓝牙耳机支持音量控件，然后音频驱动程序应卷节点拓扑中加入其 KS。 音频驱动程序的卷属性处理程序将上述 IOCLTs 发送到蓝牙 HFP 驱动程序来处理卷。

-   如果将蓝牙耳机不实现硬件卷和编解码器 （或 DSP） 具有硬件卷，音频驱动程序应处理的编解码器 （或 DSP） 上的音量控制。

-   蓝牙耳机和音频设备没有硬件音量控件，如果没有卷节点应会显示，Windows 将插入软件卷控制节点。

静音节点是可选的。 音频驱动程序应实现静音节点，当且仅当 DSP 或音频编解码器提供了将调节到静音绕过 PCM 信号，然后再将它传递到蓝牙控制器的功能。 静音节点支持[ **KSPROPERTY\_音频\_设为静音**](https://msdn.microsoft.com/library/windows/hardware/ff537293)。

## <a name="span-idpropertyrequestsspanspan-idpropertyrequestsspanspan-idpropertyrequestsspanproperty-requests"></a><span id="Property_requests"></span><span id="property_requests"></span><span id="PROPERTY_REQUESTS"></span>属性请求


音频驱动程序将使用以下 KS 属性来获取有关任何音频插孔的信息或插孔中音频的路径。 和音频驱动程序还可以使用相应的属性请求来建立或断开任何蓝牙音频设备的连接中的音频的路径。

**KSPROPERTY\_JACK\_说明**

此属性返回[ **KSJACK\_说明**](https://msdn.microsoft.com/library/windows/hardware/ff537136)结构。 音频驱动程序应设置[ **KSPROPERTY\_JACK\_说明**](https://msdn.microsoft.com/library/windows/hardware/ff537364)字段，如下所示。
ChannelMapping = KSAUDIO\_演讲者\_MONO 颜色 = 0 ConnectionType = eConnTypeOtherDigital 地理位置 = eGeoLocNotApplicable GenLocation = eGenLocOther PortConnection = ePortConnUnknown IsConnected = &lt; *对于当前连接状态为 BOOL* &gt; **KSPROPERTY\_JACK\_DESCRIPTION2**

此属性返回[ **KSJACK\_DESCRIPTION2** ](https://msdn.microsoft.com/library/windows/hardware/ff537138)结构。 音频驱动程序应设置[ **KSPROPERTY\_JACK\_DESCRIPTION2** ](https://msdn.microsoft.com/library/windows/hardware/ff537365)字段，如下所示。
DeviceStateInfo = 0 JackCapabilities = JACKDESC2\_是否存在\_检测\_功能**KSPROPERTY\_ONESHOT\_重新连接**

支持音频驱动程序的筛选器应[ **KSPROPERTY\_ONESHOT\_重新连接**](https://msdn.microsoft.com/library/windows/hardware/ff537369)。 若要创建和初始化此结构，音频驱动程序发送[ **IOCTL\_BTHHFP\_设备\_请求\_CONNECT** ](https://msdn.microsoft.com/library/windows/hardware/dn265114) HFP 驱动程序。 HFP 驱动程序完成此请求，然后尝试以异步方式连接到 Bluetooth 音频设备。
**KSPROPERTY\_ONESHOT\_断开连接**

支持音频驱动程序的筛选器应[ **KSPROPERTY\_ONESHOT\_断开连接**](https://msdn.microsoft.com/library/windows/hardware/hh706181)。 若要创建和初始化此结构，音频驱动程序发送[ **IOCTL\_BTHHFP\_设备\_请求\_断开连接**](https://msdn.microsoft.com/library/windows/hardware/dn265115) HFP 驱动程序。 HFP 驱动程序完成此请求，然后尝试以异步方式从蓝牙音频设备断开连接。
当音频驱动程序支持以下属性时，在控制面板中的声音对话框公开 HFP 终结点的连接和断开连接命令。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[理论上的操作](theory-of-operation.md)  



