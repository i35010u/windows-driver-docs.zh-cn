---
title: 插孔说明属性
description: 插孔说明属性
ms.assetid: 6398efc9-4435-4234-bd72-1ed0f96c9f9f
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: b8f579dab6541c820f0cc1af2be276b4801c2cd5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333382"
---
# <a name="jack-description-property"></a>插孔说明属性


在 Windows Vista 及更高版本， [ **KSPROPERTY\_JACK\_说明**](https://msdn.microsoft.com/library/windows/hardware/ff537364)属性描述音频适配器上的音频插孔或其他物理连接器。 属性值描述 jack 的颜色、 jack、 连接器类型和其他 jack 功能的物理位置。 此信息旨在帮助用户查找有关等麦克风、 耳机或扬声器音频终结点设备中插入正确的插孔。 有关详细信息，请参阅[音频终结点设备](https://go.microsoft.com/fwlink/p/?linkid=130876)。

音频的适配器上 KS 筛选器是否支持 KSPROPERTY\_JACK\_DESCRIPTION 属性，Windows 多媒体控件面板中，Mmsys.cpl，显示器筛选器的桥的插孔信息插针。 桥 pin 表示音频的终结点设备的连接 （通常情况下，插孔）。 尽管属性值包含一个 pin （或相反，则插孔与 pin 关联） 有关的信息，该属性是属性的筛选器，而不是 pin。 有关桥的 pin 的详细信息，请参阅[音频筛选器关系图](audio-filter-graphs.md)。 有关筛选器属性和 pin 属性的详细信息，请参阅[筛选器、 Pin 和节点属性](filter--pin--and-node-properties.md)。

音频应用程序可以获取 KSPROPERTY\_JACK\_说明属性值，通过调用音频终结点设备**IKsJackDescription::GetJackDescription**中 DeviceTopology 方法API。 例如，应用程序可以使用 jack 信息以帮助用户区分插入来自麦克风插入橙色的 XLR 插孔绿色 XLR 插孔麦克风。 有关 DeviceTopology API 的详细信息，请参阅[设备拓扑](https://go.microsoft.com/fwlink/p/?linkid=130878)。

Microsoft HD Audio 类驱动程序自动构造 KSPROPERTY\_JACK\_说明属性值从它从 HD Audio 编解码器中的 pin 配置寄存器中读取的数据。 但是，任何基于 KS 的音频驱动程序可以在其筛选器自动化表中实现支持此属性。 HD Audio 类驱动程序有关的详细信息，请参阅[HD Audio 和 UAA](hd-audio-and-uaa.md)。 有关 pin 配置注册表的详细信息，请参阅[高清晰度音频设备的插针配置指南](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/PinConfig.doc)白皮书。

通过一个或多个插孔，音频终结点设备可以连接到桥 pin。 例如，一组 （两个通道） 立体扬声器需要有一个插孔，但 5.1 环绕声扬声器的集需要三个插孔 （假定每个插座处理两个六个声道）。

中包含的说明每个插座[ **KSJACK\_说明**](https://msdn.microsoft.com/library/windows/hardware/ff537136)结构。 例如，KSPROPERTY\_JACK\_有一个 jack 的音频端点设备的说明属性值包含一个 KSJACK\_描述结构，但有三个插座的终结点设备的属性值包含三个 KSJACK\_描述结构。 在任一情况下，KSJACK\_描述结构或结构中的属性值的前面有[ **KSMULTIPLE\_项**](https://msdn.microsoft.com/library/windows/hardware/ff563441)结构，它指定的大小属性值。 有关详细信息，请参阅[ **KSPROPERTY\_JACK\_说明**](https://msdn.microsoft.com/library/windows/hardware/ff537364)。

Jack 信息是特别有用，可帮助用户来区分连接到多渠道扬声器配置的插孔。 下面的代码示例显示了一个数组 KSJACK\_音频驱动程序使用来描述一套 5.1 环绕扬声器的三个插孔的描述结构：

```cpp
KSJACK_DESCRIPTION ar_5dot1_Jacks[] =
{
    // Jack 1
    {
        (SPEAKER_FRONT_LEFT | SPEAKER_FRONT_RIGHT), // ChannelMapping (L,R)
        RGB(0,255,0),       // Color (green)
        eConnType3Point5mm, // ConnectionType
        eGeoLocRear,        // GeoLocation
        eGenLocPrimaryBox,  // GenLocation
        ePortConnJack,      // PortConnection
        TRUE                // IsConnected
    },
    // Jack 2
    {
        (SPEAKER_FRONT_CENTER | SPEAKER_LOW_FREQUENCY), // (C,Sub)
        RGB(0,0,255),       // (red)
        eConnType3Point5mm,
        eGeoLocRear,
        eGenLocPrimaryBox,
        ePortConnJack,
        TRUE
    },
    // Jack 3
    {
        (SPEAKER_SIDE_LEFT | SPEAKER_SIDE_RIGHT),  // (SL,SR)
        RGB(0,255,255),     // (yellow)
        eConnType3Point5mm,
        eGeoLocRear,
        eGenLocPrimaryBox,
        ePortConnJack,
        TRUE
    }
};
```

如果音频硬件可以检测是否在插入设备，该驱动程序会动态更新以指示是否在当前插入设备此成员的值 (**，则返回 TRUE**) 或拔出 (**FALSE**)

在前面的代码示例中， **IsConnected**每个数组元素中的成员设置为**TRUE**来指示终结点设备是否已插入插孔。 但是，如果硬件缺少 jack 存在检测**IsConnected**必须始终设置为**TRUE**、 是否有设备插入到的插孔。 若要删除此双的含义而得出的多义性 **，则返回 TRUE**返回值，客户端应用程序可以调用[IKsJackDescription2::GetJackDescription2](https://go.microsoft.com/fwlink/p/?linkid=143698)读取的 JackCapabilities 标志[ **KSJACK\_DESCRIPTION2** ](https://msdn.microsoft.com/library/windows/hardware/ff537138)结构。 如果此标志有 JACKDESC2\_是否存在\_检测\_功能位集，它指示终结点，实际上支持 jack 在场检测。 在这种情况下，值**IsConnected**成员可以解释为应用的插孔插入状态的准确映像。

标头文件 Wingdi.h 在 Windows SDK 中定义的 RGB 宏，将出现在前面的结构。

此外，jack 描述的数组可以用于显示两个或多个插孔是功能上等效于彼此。 在下面的代码示例中，音频驱动程序将合并到一个数组，以向用户指示两个插座执行相同的信号的插孔说明为黄色 RCA 插孔和黑色数字光学 jack:

```cpp
KSJACK_DESCRIPTION ar_SPDIF_Jacks[] =
{
    // Jack 1
    {
        (SPEAKER_FRONT_LEFT | SPEAKER_FRONT_RIGHT), // ChannelMapping (L,R)
        RGB(0,255,255),         // Color (yellow)
        eConnTypeRCA,           // ConnectionType (RCA)
        eGeoLocRear,            // GeoLocation
 eGenLocPrimaryBox,   // GenLocation
        ePortConnJack,       // PortConnection
        TRUE                    // IsConnected
    },
    // Jack 2
    {
        (SPEAKER_FRONT_LEFT | SPEAKER_FRONT_RIGHT), // (L,R)
        RGB(0,0,0),             // (black)
        eConnTypeOptical,       // (optical)
        eGeoLocRear,
 eGenLocPrimaryBox,
        ePortConnJack,
        TRUE
    }
};
```

在前面的代码示例的值**ChannelMapping**成员中两个 KSJACK\_描述结构是否相同。

WDK 中的"简单"MSVAD 示例驱动程序 (在示例目录 Src\\音频\\Msvad\\简单) 可以进行适配化以便支持 KSPROPERTY\_JACK\_DESCRIPTION 属性。 此示例驱动程序是方便演示如何使用该属性，因为它不需要实际的硬件。 因此，它可以安装在运行 Windows 的任何计算机上。 (但是，只有 Windows Vista 和更高版本操作系统提供完全支持 KSPROPERTY\_JACK\_DESCRIPTION 属性。)有关此示例的详细信息，请参阅[Windows 驱动程序工具包示例](https://msdn.microsoft.com/library/windows/hardware/ff554118)。

简单 MSVAD 示例拓扑筛选器定义三个桥 pin。 下表列出了这些引脚。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Pin ID</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSPIN_TOPO_SYNTHIN_SOURCE</p></td>
<td align="left"><p>MIDI 输入的插孔</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPIN_TOPO_MIC_SOURCE</p></td>
<td align="left"><p>麦克风输入的插孔</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSPIN_TOPO_LINEOUT_DEST</p></td>
<td align="left"><p>立体扬声器输出插孔</p></td>
</tr>
</tbody>
</table>

 

此主题的其余部分说明如何修改简单 MSVAD 示例驱动程序提供三个桥 pin 的插孔信息。

首先，可以按以下方式指定这些引脚的插孔信息：

```cpp
// Describe MIDI input jack (pin ID = KSPIN_TOPO_SYNTHIN_SOURCE).
static KSJACK_DESCRIPTION SynthIn_Jack[] =
{
    {
        0,                  // ChannelMapping
        RGB(255,255,0),    // Color (cyan)
 eConnType3Point5mm, // ConnectionType
        eGeoLocRear,        // GeoLocation
        eGenLocPrimaryBox,  // GenLocation
        ePortConnJack,      // PortConnection
        TRUE                // IsConnected
    }
};

// Describe microphone jack (pin ID = KSPIN_TOPO_MIC_SOURCE).
static KSJACK_DESCRIPTION MicIn_Jack[] =
{
    {
        0,
        RGB(0,128,255),   // (orange)
 eConnType3Point5mm,
        eGeoLocFront,
        eGenLocPrimaryBox,
        ePortConnJack,
        TRUE
    }
};

// Describe stereo speaker jack (pin ID = KSPIN_TOPO_LINEOUT_DEST).
static KSJACK_DESCRIPTION LineOut_Jack[] =
{
    {
        (SPEAKER_FRONT_LEFT | SPEAKER_FRONT_RIGHT), // ChannelMapping (L,R)
        RGB(0,255,0),       // (green)
 eConnType3Point5mm,
        eGeoLocRear,
        eGenLocPrimaryBox,
        ePortConnJack,
        TRUE
    }
};
```

前面的代码示例设置**ChannelMapping**为 0 的两个捕获针的成员。 仅模拟呈现 pin 应具有非零**ChannelMapping**值。

简单 MSVAD 示例的主修改是将以下属性处理程序添加到示例文件 Mintopo.cpp 中的拓扑微型端口实现：

```cpp
#define ARRAY_LEN(a)  sizeof(a)/sizeof(a[0]);
#define MAXIMUM_VALID_PIN_ID  KSPIN_TOPO_WAVEIN_DEST

NTSTATUS
CMiniportTopology::PropertyHandlerJackDescription(
               IN PPCPROPERTY_REQUEST PropertyRequest)
{
    PAGED_CODE();

    ASSERT(PropertyRequest);

    DPF_ENTER(("[PropertyHandlerJackDescription]"));

    NTSTATUS ntStatus = STATUS_INVALID_DEVICE_REQUEST;
    ULONG nPinId = (ULONG)-1;

    if (PropertyRequest->InstanceSize >= sizeof(ULONG))
    {
        nPinId = *((PULONG)(PropertyRequest->Instance));

        if (nPinId > MAXIMUM_VALID_PIN_ID)
        {
            ntStatus = STATUS_INVALID_PARAMETER;
        }
        else if (PropertyRequest->Verb & KSPROPERTY_TYPE_BASICSUPPORT)
        {
            ntStatus = PropertyHandler_BasicSupport(
                            PropertyRequest,
                            KSPROPERTY_TYPE_BASICSUPPORT | KSPROPERTY_TYPE_GET,
                            VT_ILLEGAL);
        }
        else
        {
            PKSJACK_DESCRIPTION pJack = NULL;
            ULONG cJacks = 0;

            switch (nPinId)
            {
            case KSPIN_TOPO_SYNTHIN_SOURCE:
                pJack = SynthIn_Jack;
                cJacks = ARRAY_LEN(SynthIn_Jack);
                break;
            case KSPIN_TOPO_MIC_SOURCE:
                pJack = MicIn_Jack;
                cJacks = ARRAY_LEN(MicIn_Jack);
                break;
            case KSPIN_TOPO_LINEOUT_DEST:
                pJack = LineOut_Jack;
                cJacks = ARRAY_LEN(LineOut_Jack);
                break;
            default:
                break;
            }

            ULONG cbNeeded = sizeof(KSMULTIPLE_ITEM) +
                             sizeof(KSJACK_DESCRIPTION) * cJacks;

            if (PropertyRequest->ValueSize == 0)
            {
                PropertyRequest->ValueSize = cbNeeded;
                ntStatus = STATUS_BUFFER_OVERFLOW;
            }
            else if (PropertyRequest->ValueSize < cbNeeded)
            {
                ntStatus = STATUS_BUFFER_TOO_SMALL;
            }
            else if (PropertyRequest->Verb & KSPROPERTY_TYPE_GET)
            {
                PKSMULTIPLE_ITEM pMI = (PKSMULTIPLE_ITEM)PropertyRequest->Value;

                pMI->Size = cbNeeded;
                pMI->Count = cJacks;

                // Copy jack description structure into Value buffer.
                // RtlCopyMemory correctly handles the case Length=0.
                PKSJACK_DESCRIPTION pDesc = (PKSJACK_DESCRIPTION)(pMI + 1);

                RtlCopyMemory(pDesc, pJack, pMI->Size * pMI->Count);

                ntStatus = STATUS_SUCCESS;
            }
        }
    }

    return ntStatus;
}

NTSTATUS
PropertyHandler_TopoFilter(IN PPCPROPERTY_REQUEST PropertyRequest)
{
    PAGED_CODE();

    ASSERT(PropertyRequest);

    DPF_ENTER(("[PropertyHandler_TopoFilter]"));

    // PropertyRequest structure is filled by PortCls.
    // MajorTarget is a pointer to miniport object for miniports.
    //
    NTSTATUS ntStatus = STATUS_INVALID_DEVICE_REQUEST;
    PCMiniportTopology pMiniport = (PCMiniportTopology)PropertyRequest->MajorTarget;

    if (IsEqualGUIDAligned(*PropertyRequest->PropertyItem->Set, KSPROPSETID_Jack) &&
        (PropertyRequest->PropertyItem->Id == KSPROPERTY_JACK_DESCRIPTION))
    {
        ntStatus = pMiniport->PropertyHandlerJackDescription(PropertyRequest);
    }

    return ntStatus;
}
```

前面的代码示例是指三个 KSJACK\_说明变量-SynthIn\_Jack、 MicIn\_插孔和线路输出\_Jack-之前定义。 如果客户端会查询的一个有效的 pin，但其中一个 jack 说明的不是桥 pin （并因此没有 jack 说明） 的筛选器，查询将成功 (，其状态代码状态\_成功)，但属性处理程序返回空插孔描述包含 KSMULTIPLE\_项结构和其他任何内容。 如果客户端指定的 pin 无效 ID （用于标识不存在的 pin），该处理程序将返回状态代码状态\_无效\_参数。

对简单 MSVAD 示例的两个其他修改都需要支持 KSPROPERTY\_JACK\_DESCRIPTION 属性。 这些是：

-   添加的声明**PropertyHandlerJackDescription**向标头文件 Mintopo.h 中 CMiniportTopology 类定义前面的代码示例中的方法。

-   实现用于拓扑筛选器的自动化表并加载到此表的地址**AutomationTable**的成员[ **PCFILTER\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff537694)标头文件 Toptable.h 中的结构。 此结构的命名**MiniportFilterDescriptor**。

若要实现自动化的筛选器表，插入以下代码到标头文件 Toptable.h (的定义前面**MiniportFilterDescriptor**):

```cpp
static PCPROPERTY_ITEM PropertiesTopoFilter[] =
{
    {
        &KSPROPSETID_Jack,
        KSPROPERTY_JACK_DESCRIPTION,
        KSPROPERTY_TYPE_GET | KSPROPERTY_TYPE_BASICSUPPORT,
        PropertyHandler_TopoFilter
    }
};

DEFINE_PCAUTOMATION_TABLE_PROP(AutomationTopoFilter, PropertiesTopoFilter);
```

在前面的代码示例中，**处理程序**的成员[ **PCPROPERTY\_项**](https://msdn.microsoft.com/library/windows/hardware/ff537722)结构包含了的属性处理程序的函数指针上一步中添加到 Mintopo.cpp。 若要使属性处理程序可访问标头文件中，插入**extern**函数声明为 PropertyHandler\_TopoFilter 开头的标头文件。

Jack description 属性的详细信息，请参阅[Jack 说明动态音频子设备](jack-descriptions-for-dynamic-audio-subdevices.md)。

 

 




