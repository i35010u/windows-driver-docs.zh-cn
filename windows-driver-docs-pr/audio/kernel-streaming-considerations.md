---
title: 内核流式处理注意事项
description: 内核流式处理注意事项主题阐明了与蓝牙绕过音频流相关的要求和其他特别注意事项。
ms.assetid: CFC4ACA0-050D-48E1-AA6A-7649040EBF7A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 314508710c729d65afb3a63fe265f303d4b603f9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207047"
---
# <a name="kernel-streaming-considerations"></a>内核流式处理注意事项


内核流式处理注意事项主题阐明了除所有音频驱动程序以外的要求和其他特殊注意事项。 这些是与蓝牙绕过音频流相关的内核流式处理注意事项。

音频驱动程序应该完全支持 WaveRT 端口驱动程序，包括 "请求模式"。 有关详细信息，请参阅 [WaveRT 端口驱动程序简介](introducing-the-wavert-port-driver.md)。 尽管不要求为同步连接实现硬件音频引擎 (SCO) 绕过输出，但不会对此造成任何伤害。

格式支持的 Windows 徽标要求包括蓝牙例外。

音频驱动程序应支持通过 sideband 硬件可以使用的格式。 这通常是 8KHz mono 音频流。

## <a name="span-idtopologyspanspan-idtopologyspanspan-idtopologyspantopology"></a><span id="Topology"></span><span id="topology"></span><span id="TOPOLOGY"></span>拓扑


所有蓝牙免提设备都支持捕获和呈现。 因此，音频驱动程序应公开用于免提设备的内核流式处理 (KS) 拓扑，如下面的关系图中所示，支持呈现和捕获。

![显示音频驱动程序为免提设备公开的 ks 拓扑的关系图，以支持呈现和捕获。](images/btth-bypass-topology.png)

**注意**   音频驱动程序开发人员可以选择是为捕获路径和呈现路径还是单独的筛选器实施单个筛选器。 但是，HFP 设备仅允许 GUID \_ DEVINTERFACE \_ 蓝牙 \_ HFP \_ SCO \_ HCIBYPASS 设备接口上的单个文件对象。 因此，使用两个筛选器的设计需要允许两个筛选器共享单个文件对象。

 

DAC 和 ADC 节点表示模拟/数字转换，但不支持任何 KS 属性。

卷节点通过将 SETVOLUME 和 GETVOLUMESTATUSUPDATE IOCTLs 发送到 HFP 驱动程序来支持 [**KSPROPERTY \_ AUDIO \_ VOLUMELEVEL**](./ksproperty-audio-volumelevel.md) 和 [**KSEVENT \_ 控制 \_ 更改**](./ksevent-control-change.md) 。

应按如下所示实现卷节点：

-   如果蓝牙耳机支持音量控制，则音频驱动程序应在其 KS 拓扑中包含一个卷节点。 音频驱动程序的卷属性处理程序将上述 IOCLTs 发送到蓝牙 HFP 驱动程序来处理该卷。

-   如果蓝牙耳机未实现硬件卷，且编解码器 (或 DSP) 具有硬件卷，则音频驱动程序应处理编解码器 (或 DSP) 上的音量控制。

-   如果蓝牙耳机和音频设备没有硬件音量控制，则不会显示任何卷节点，Windows 将插入软件卷控制节点。

静音节点是可选的。 当且仅当 DSP 或音频编解码器在将绕过 PCM 信号传递到 Bluetooth 控制器之前，该功能应实现静音节点。 静音节点支持 [**KSPROPERTY \_ 音频 \_ 静音**](./ksproperty-audio-mute.md)。

## <a name="span-idproperty_requestsspanspan-idproperty_requestsspanspan-idproperty_requestsspanproperty-requests"></a><span id="Property_requests"></span><span id="property_requests"></span><span id="PROPERTY_REQUESTS"></span>属性请求


音频驱动程序使用以下 KS 属性来获取有关音频路径中的任何音频插孔或插孔的信息。 音频驱动程序还可以使用相应的属性请求来建立或断开与音频路径中任何蓝牙音频设备的连接。

**KSPROPERTY \_ 插孔 \_ 说明**

此属性返回 [**KSJACK \_ 说明**](./ksjack-description.md) 结构。 音频驱动程序应设置 [**KSPROPERTY \_ 插座 \_ 描述**](./ksproperty-jack-description.md) 字段，如下所示。
ChannelMapping = KSAUDIO \_ 发言人 \_ MONO Color = 0 ConnectionType = eConnTypeOtherDigital 地理位置 = eGeoLocNotApplicable GenLocation = eGenLocOther PortConnection = ePortConnUnknown connectionmultiplexer.isconnected = &lt; *BOOL 用于当前连接状态* &gt; **KSPROPERTY \_ 插孔 \_ DESCRIPTION2**

此属性返回 [**KSJACK \_ DESCRIPTION2**](./ksjack-description2.md) 结构。 音频驱动程序应设置 [**KSPROPERTY \_ 插座 \_ DESCRIPTION2**](./ksproperty-jack-description2.md) 字段，如下所示。
DeviceStateInfo = 0 JackCapabilities = JACKDESC2 \_ 状态 \_ 检测 \_ 功能 **KSPROPERTY \_ ONESHOT \_ 重新连接**

音频驱动程序的筛选器应支持 [**KSPROPERTY \_ ONESHOT \_ 重新连接**](./ksproperty-oneshot-reconnect.md)。 若要创建并初始化此结构，音频驱动程序会将 [**IOCTL \_ BTHHFP \_ 设备 \_ 请求 \_ 连接**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_request_connect) 发送到 HFP 驱动程序。 HFP 驱动程序完成此请求，然后尝试以异步方式连接到蓝牙音频设备。
**KSPROPERTY \_ ONESHOT \_ 断开连接**

音频驱动程序的筛选器应支持 [**KSPROPERTY \_ ONESHOT \_ 断开连接**](./ksproperty-oneshot-disconnect.md)。 若要创建并初始化此结构，音频驱动程序会将 [**IOCTL \_ BTHHFP \_ 设备 \_ 请求 \_ 断开连接**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_request_disconnect) 到 HFP 驱动程序。 HFP 驱动程序完成此请求，然后尝试从蓝牙音频设备异步断开连接。
当音频驱动程序支持这些属性时，控制面板中的 "声音" 对话框会显示 HFP 终结点的连接和断开连接命令。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[操作理论](theory-of-operation.md)