---
title: 插孔说明属性
description: 插孔说明属性
ms.assetid: 6398efc9-4435-4234-bd72-1ed0f96c9f9f
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: dfea9a4cb1a229d997435ff597fc11d233117705
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833196"
---
# <a name="jack-description-property"></a>插孔说明属性


在 Windows Vista 和更高版本中， [**KSPROPERTY\_插孔\_DESCRIPTION**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-jack-description)属性描述音频适配器上的音频插孔或其他物理连接器。 属性值描述插孔、插孔的物理位置、连接器类型和其他插孔功能的颜色。 此信息的目的是帮助用户找到正确的插孔来插入音频终结点设备，如麦克风、耳机或扬声器。 有关详细信息，请参阅[音频终结点设备](https://go.microsoft.com/fwlink/p/?linkid=130876)。

如果音频适配器上的 KS 筛选器支持 KSPROPERTY\_插孔\_DESCRIPTION 属性，则 Windows 多媒体控制面板 Mmsys 将在筛选器上显示桥接的插座信息。 桥接 pin 表示音频终结点设备的连接（通常是插孔）。 尽管属性值包含有关 pin （或与该 pin 关联的插孔）的信息，但该属性是筛选器的属性，而不是 pin。 有关桥接 pin 的详细信息，请参阅[音频筛选器图](audio-filter-graphs.md)。 有关筛选器属性和 pin 属性的详细信息，请参阅[筛选器、固定和节点属性](filter--pin--and-node-properties.md)。

音频应用程序可以通过在 DeviceTopology API 中调用**IKsJackDescription：： GetJackDescription**方法来获取音频终结点设备的 KSPROPERTY\_插孔\_DESCRIPTION 属性值。 例如，应用程序可以使用插座信息来帮助用户区分插入到绿色 XLR 插孔的麦克风和插入橙色 XLR 插孔的麦克风。 有关 DeviceTopology API 的详细信息，请参阅[设备拓扑](https://go.microsoft.com/fwlink/p/?linkid=130878)。

Microsoft 高质音频类驱动程序会自动构造 KSPROPERTY\_插孔\_说明属性值，该属性值来自从在 HD 音频编解码器中的 pin 配置注册读取的数据。 但是，任何基于 KS 的音频驱动程序都可以在其筛选器自动化表中实现对此属性的支持。 有关 HD 音频类驱动程序的详细信息，请参阅[高质音频和 UAA](hd-audio-and-uaa.md)。 有关 pin 配置注册的详细信息，请参阅[高清晰音频设备的固定配置准则](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/PinConfig.doc)白皮书。

音频终结点设备可以通过一个或多个插座连接到桥接。 例如，一组（两通道）立体声扬声器需要一个插孔，但一组5.1 环绕声扬声器需要三个插孔（假设每个插座处理六个通道中的两个）。

每个插孔的说明都包含在[**KSJACK\_说明**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description)结构中。 例如，具有一个插孔的音频终结点设备的 KSPROPERTY\_插孔\_DESCRIPTION 属性值包含一个 KSJACK\_描述结构，但具有三个插座的终结点设备的属性值包含三个 KSJACK\_说明结构。 在任一情况下，属性值中的 KSJACK\_说明结构或结构前面都有一个[**KSMULTIPLE\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)结构，该结构指定属性值的大小。 有关详细信息，请参阅[**KSPROPERTY\_插孔\_说明**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-jack-description)。

插座信息对于帮助用户区分连接到多通道扬声器配置的插孔特别有用。 下面的代码示例显示了一个 KSJACK\_说明结构的数组，音频驱动程序使用该结构来描述一组5.1 环绕扬声器的三个插座：

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

如果音频硬件检测到设备是否已插入，驱动程序会动态更新此成员的值，以指示设备当前是否已插入（**TRUE**）或已拔出（**FALSE**）

在上面的代码示例中，每个数组元素中的**connectionmultiplexer.isconnected**成员设置为**TRUE** ，以指示终结点设备已插入插孔。 但是，如果硬件缺少插孔存在检测，则必须始终将**connectionmultiplexer.isconnected**设置为**TRUE**，无论是否有设备插入插孔。 若要从**真正**的返回值的这一双重含义中消除产生的多义性，客户端应用程序可以调用[IKsJackDescription2：： GetJackDescription2](https://go.microsoft.com/fwlink/p/?linkid=143698)来读取[**KSJACK\_DESCRIPTION2**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description2)的 JackCapabilities 标志构造. 如果此标志具有 JACKDESC2\_存在\_检测\_功能位，则表明终结点确实支持插孔状态检测。 在这种情况下，可以将**connectionmultiplexer.isconnected**成员的值解释为插孔插入状态的准确反射。

在 Windows SDK 中的头文件 Wingdi 中定义了前面的结构中显示的 RGB 宏。

此外，插孔说明的数组可用于显示两个或更多个插座在功能上是等效的。 在下面的代码示例中，音频驱动程序将黄色 RCA 插孔和黑色数字光学插孔的插孔说明合并为一个阵列，以向用户指明两个插孔是否具有相同的信号：

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

在上面的代码示例中，两个 KSJACK\_说明结构中的**ChannelMapping**成员的值相同。

WDK 中的 "Simple" MSVAD 示例驱动程序（在示例目录 Src\\音频\\Msvad\\Simple）可以改编为支持 KSPROPERTY\_插座\_DESCRIPTION 属性。 此示例驱动程序可用于演示属性的使用，因为它不需要实际硬件。 因此，它可以安装在任何运行 Windows 的计算机上。 （但是，只有 Windows Vista 和更高版本的操作系统才为 KSPROPERTY\_插孔\_DESCRIPTION 属性提供完全支持。）有关此示例的详细信息，请参阅[Windows 驱动程序工具包示例](https://docs.microsoft.com/windows-hardware/drivers/samples/index)。

简单 MSVAD 示例的拓扑筛选器定义了三个桥接 pin。 下表列出了这些针脚。

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
<td align="left"><p>MIDI 输入插孔</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPIN_TOPO_MIC_SOURCE</p></td>
<td align="left"><p>麦克风输入插孔</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSPIN_TOPO_LINEOUT_DEST</p></td>
<td align="left"><p>立体声扬声器输出插孔</p></td>
</tr>
</tbody>
</table>

 

本主题的其余部分说明如何修改简单的 MSVAD 示例驱动程序，以便为三个桥接 pin 提供插孔信息。

首先，可以按如下所示指定这些 pin 的插孔信息：

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

前面的代码示例将两个捕获 pin 的**ChannelMapping**成员设置为0。 只有模拟呈现 pin 应具有非零的**ChannelMapping**值。

简单的 MSVAD 示例的主要修改是将以下属性处理程序添加到示例文件 Mintopo 中的拓扑微端口实现：

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

前面的代码示例指的是之前定义的三个 KSJACK\_说明变量-SynthIn\_插孔、MicIn\_插孔和 LineOut\_插孔。 如果客户端查询对有效 pin 的插孔说明的筛选器，但不是桥接（因此没有插孔说明），则查询将成功（状态代码状态\_成功），但属性处理程序返回空的插孔说明由 KSMULTIPLE\_项结构和其他内容组成。 如果客户端指定了无效的 pin ID （用于标识不存在的 pin），则处理程序将返回状态代码状态\_无效\_参数。

若要支持 KSPROPERTY\_插孔\_DESCRIPTION 属性，需要另外两处修改简单的 MSVAD 示例。 它们是：

-   将前面代码示例中的**PropertyHandlerJackDescription**方法的声明添加到头文件 Mintopo 中的 CMiniportTopology 类定义。

-   实现拓扑筛选器的自动化表，并将此表的地址加载到头文件 Toptable 中[**PCFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)结构的**AutomationTable**成员中。 此结构名为**MiniportFilterDescriptor**。

若要实现筛选器的自动化表，请在头文件 Toptable 中插入以下代码（在**MiniportFilterDescriptor**的定义之前）：

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

在上面的代码示例中， [**PCPROPERTY\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcproperty_item)结构的**处理程序**成员包含一个函数指针，该指针指向在上一步中添加到 Mintopo 的属性处理程序。 若要使属性处理程序可从头文件访问，请在标头文件的开头插入 PropertyHandler\_TopoFilter 的**extern**函数声明。

有关 "插座说明" 属性的详细信息，请参阅[Subdevices 的插座说明](jack-descriptions-for-dynamic-audio-subdevices.md)。

 

 




