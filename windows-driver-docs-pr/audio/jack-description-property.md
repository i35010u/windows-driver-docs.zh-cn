---
title: 插孔说明属性
description: 插孔说明属性
ms.assetid: 6398efc9-4435-4234-bd72-1ed0f96c9f9f
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 789d07736a63304e86d48258ecb36451c40aad02
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209073"
---
# <a name="jack-description-property"></a>插孔说明属性


在 Windows Vista 和更高版本中， [**KSPROPERTY \_ 插孔 \_ 说明**](./ksproperty-jack-description.md) 属性描述音频适配器上的音频插孔或其他物理连接器。 属性值描述插孔、插孔的物理位置、连接器类型和其他插孔功能的颜色。 此信息的目的是帮助用户找到正确的插孔来插入音频终结点设备，如麦克风、耳机或扬声器。 有关详细信息，请参阅 [音频终结点设备](/windows/win32/coreaudio/audio-endpoint-devices)。

如果音频适配器上的 KS 筛选器支持 KSPROPERTY \_ 插孔 \_ 说明属性，则 Windows 多媒体控制面板 Mmsys.cpl 将显示该筛选器上桥接的插孔信息。 网桥表示连接 (通常是音频终结点设备的插孔) 。 尽管属性值包含与 pin) 关联的 (的信息，或者与该 pin 相关联的插孔，但该属性是筛选器的属性，而不是 pin。 有关桥接 pin 的详细信息，请参阅 [音频筛选器图](audio-filter-graphs.md)。 有关筛选器属性和 pin 属性的详细信息，请参阅 [筛选器、固定和节点属性](filter--pin--and-node-properties.md)。

音频应用程序可以 \_ \_ 通过在 DeviceTopology API 中调用 **IKsJackDescription：： GetJackDescription** 方法来获取音频终结点设备的 KSPROPERTY 插孔说明属性值。 例如，应用程序可以使用插座信息来帮助用户区分插入到绿色 XLR 插孔的麦克风和插入橙色 XLR 插孔的麦克风。 有关 DeviceTopology API 的详细信息，请参阅 [设备拓扑](/windows/win32/coreaudio/device-topologies)。

Microsoft 高质音频类驱动程序会自动构造 \_ 从其读取的数据中的 KSPROPERTY 插孔 \_ 说明属性值。 但是，任何基于 KS 的音频驱动程序都可以在其筛选器自动化表中实现对此属性的支持。 有关 HD 音频类驱动程序的详细信息，请参阅 [高质音频和 UAA](hd-audio-and-uaa.md)。 有关 pin 配置注册的详细信息，请参阅 [高清晰音频设备的 Pin 配置指南](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/PinConfig.doc) 白皮书。

音频终结点设备可以通过一个或多个插座连接到桥接。 例如，一组 (两通道) 立体声扬声器需要一个插孔，但一组5.1 环绕声扬声器需要三个插座， (假设每个插座均处理六个通道中的两个) 。

每个插孔的说明都包含在 [**KSJACK \_ 说明**](./ksjack-description.md) 结构中。 例如， \_ \_ 具有一个插孔的音频终结点设备的 KSPROPERTY 插孔说明属性值包含一个 KSJACK \_ 说明结构，但具有三个插孔的终结点设备的属性值包含三个 KSJACK \_ 说明结构。 在任一情况下， \_ 属性值中的 KSJACK 说明结构或结构前面都有一个 [**KSMULTIPLE \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item) 结构，该结构指定属性值的大小。 有关详细信息，请参阅 [**KSPROPERTY \_ 插座 \_ 说明**](./ksproperty-jack-description.md)。

插座信息对于帮助用户区分连接到多通道扬声器配置的插孔特别有用。 下面的代码示例显示了一个 KSJACK \_ 说明结构数组，音频驱动程序使用该结构来描述一组5.1 环绕发言人扬声器的三个插座：

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

如果音频硬件检测到设备是否已插入，驱动程序会动态更新此成员的值，以指示设备当前是否插入 (**TRUE**) 或拔下 (**FALSE**) 

在上面的代码示例中，每个数组元素中的 **connectionmultiplexer.isconnected** 成员设置为 **TRUE** ，以指示终结点设备已插入插孔。 但是，如果硬件缺少插孔存在检测，则必须始终将 **connectionmultiplexer.isconnected** 设置为 **TRUE**，无论是否有设备插入插孔。 若要从 **真正** 的返回值的这一双重含义中消除产生的多义性，客户端应用程序可以调用 [IKsJackDescription2：： GetJackDescription2](/windows/win32/api/devicetopology/nf-devicetopology-iksjackdescription2-getjackdescription2) 来读取 [**KSJACK \_ DESCRIPTION2**](./ksjack-description2.md) 结构的 JackCapabilities 标志。 如果此标志具有 JACKDESC2 的 \_ " \_ 检测 \_ 功能位" 设置，则表示端点确实支持插孔状态检测。 在这种情况下，可以将 **connectionmultiplexer.isconnected** 成员的值解释为插孔插入状态的准确反射。

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

在上面的代码示例中，两个 KSJACK 说明结构中的 **ChannelMapping** 成员的值 \_ 相同。

示例目录 Src 音频 MSVAD simple) 中的 "Simple" MSVAD 示例驱动 (程序 \\ \\ \\ 可改编为支持 KSPROPERTY \_ 插座 \_ DESCRIPTION 属性。 此示例驱动程序可用于演示属性的使用，因为它不需要实际硬件。 因此，它可以安装在任何运行 Windows 的计算机上。  (但是，只有 Windows Vista 及更高版本的操作系统才提供完全支持 KSPROPERTY \_ 插座 \_ DESCRIPTION 属性 ) 。有关此示例的详细信息，请参阅 [Windows 驱动程序工具包示例](../samples/index.md)。

简单 MSVAD 示例的拓扑筛选器定义了三个桥接 pin。 下表列出了这些针脚。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Pin ID</th>
<th align="left">说明</th>
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

前面的代码示例将两个捕获 pin 的 **ChannelMapping** 成员设置为0。 只有模拟呈现 pin 应具有非零的 **ChannelMapping** 值。

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

前面的代码示例引用了前面定义的三个 KSJACK \_ 说明变量-SynthIn \_ 插座、MicIn \_ 插孔和 LineOut \_ 插孔。 如果客户端在筛选器中查询了有效 pin 的插孔说明，但其中一个不是桥接 (，因此没有) 的插孔说明，则查询将成功 (状态代码状态 " \_ 成功") ，但属性处理程序返回的是包含 KSMULTIPLE \_ 项结构而不是其他内容的空的插孔说明。 如果客户端指定了一个无效的 pin ID (标识不存在的 pin) ，则处理程序将返回状态代码状态 \_ 无效 \_ 参数。

若要支持 KSPROPERTY \_ 插座说明属性，需要另外两处修改简单的 MSVAD 示例 \_ 。 它们是：

-   将前面代码示例中的 **PropertyHandlerJackDescription** 方法的声明添加到头文件 Mintopo 中的 CMiniportTopology 类定义。

-   实现拓扑筛选器的自动化表，并将此表的地址加载到头文件 Toptable 中[**PCFILTER \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)结构的**AutomationTable**成员中。 此结构名为 **MiniportFilterDescriptor**。

若要实现筛选器的自动化表，请在 **MiniportFilterDescriptor**) 的定义之前，将以下代码插入到头文件 Toptable (：

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

在上面的代码示例中， [**PCPROPERTY \_ 项**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcproperty_item)结构的**处理程序**成员包含指向在上一步中添加到 Mintopo 的属性处理程序的函数指针。 若要使该属性处理程序可从头文件访问， **extern**请 \_ 在头文件的开头插入 PropertyHandler TopoFilter 的 extern 函数声明。

有关 "插座说明" 属性的详细信息，请参阅 [Subdevices 的插座说明](jack-descriptions-for-dynamic-audio-subdevices.md)。

 

