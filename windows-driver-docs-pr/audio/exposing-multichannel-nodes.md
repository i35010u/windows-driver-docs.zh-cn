---
title: 公开多声道节点
description: 公开多声道节点
ms.assetid: 48ee3b33-fb97-4e71-bf6f-5dbdb76aa7f8
keywords:
- 音频属性 WDK，多渠道的节点
- WDM 音频属性 WDK，多渠道的节点
- 公开多渠道的节点
- 多渠道节点 WDK 音频
- 节点 WDK 音频，多渠道
- 最小的卷级别 WDK 音频
- 最大卷级别 WDK 音频
- basic 支持查询 WDK 音频
- 范围值 WDK 音频
- SndVol32 WDK 音频
- 多个通道支持 WDK 音频
- 扬声器 WDK 音频、 多渠道节点
- 通道多渠道支持 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b6d4939617eb3deca96f9e40cd68fbf85005043
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333703"
---
# <a name="exposing-multichannel-nodes"></a>公开多声道节点


## <span id="exposing_multichannel_nodes"></span><span id="EXPOSING_MULTICHANNEL_NODES"></span>


在 Windows XP 之前的 Microsoft Windows 版本，WDM 音频驱动程序没有公开以下类型的多渠道节点的简化的方法：

[**KSNODETYPE\_卷**](https://msdn.microsoft.com/library/windows/hardware/ff537208)

[**KSNODETYPE\_静音**](https://msdn.microsoft.com/library/windows/hardware/ff537178)

[**KSNODETYPE\_音**](https://msdn.microsoft.com/library/windows/hardware/ff537205)

具体而言，没有机制存在显式查询支持的通道数的节点。 尽管有此问题的解决方法，但它们有缺点。 例如，可以使用客户端[ **KSPROPERTY\_音频\_VOLUMELEVEL** ](https://msdn.microsoft.com/library/windows/hardware/ff537309)若要以迭代方式查询卷节点的属性 ([**KSNODETYPE\_卷**](https://msdn.microsoft.com/library/windows/hardware/ff537208)) 为卷级别的每个通道-0、 1 和等等-直到该请求将返回错误，指示没有更多通道存在。 但是，此方法需要多个查询，并会导致效率低下，以处理更高版本的多声道音频设备。 在 Windows XP 和更高版本操作系统中，解决此限制之前通过定义中的两个其他标志位**标志**的成员[ **KSPROPERTY\_MEMBERSHEADER**](https://msdn.microsoft.com/library/windows/hardware/ff565189)结构，它的属性处理程序中响应 basic 支持查询的输出：

-   KSPROPERTY\_成员\_标志\_BASICSUPPORT\_多通道

    Basic 支持属性在请求期间在节点上，该处理程序设置此标志位，指示**MembersCount** KSPROPERTY 成员\_MEMBERSHEADER 包含节点支持的通道数。 对于 Windows Vista 和更高版本的 Windows 操作系统，必须为每个通道属性设置此标志。

-   KSPROPERTY\_MEMBER\_FLAG\_BASICSUPPORT\_UNIFORM

    此处理程序执行此标志位和 KSPROPERTY 之间的按位 OR\_成员\_标志\_BASICSUPPORT\_多渠道标志位，以指示单个属性值统一应用于所有在节点中的通道。 例如，如果硬件为所有通道提供了只有单个卷级别控制，卷节点的基本支持处理程序设置 KSPROPERTY\_成员\_标志\_BASICSUPPORT\_统一到标志指示此限制。 如果未设置此标志，可以独立于其他渠道的卷级别控制每个通道的音量级别。

    **请注意**   KSPROPERTY\_成员\_标志\_BASICSUPPORT\_统一标志不由 Windows Vista 操作系统。

     

微型端口驱动程序适用于 Windows XP 及更高版本，在多渠道卷节点的属性处理程序应设置 KSPROPERTY\_成员\_标志\_BASICSUPPORT\_多通道位 KSPROPERTY响应\_音频\_VOLUMELEVEL basic 支持查询。 该处理程序返回的数组[ **KSPROPERTY\_单步执行\_长**](https://msdn.microsoft.com/library/windows/hardware/ff565631)结构-一个用于公开的节点-和集的每个通道**MembersSize**到**sizeof**(KSPROPERTY\_单步执行\_长)。 每个数组元素描述通道的最小值和最大音量级别和范围内的连续值之间的增量。 可以为每个单独的通道指定不同的范围，以便可以正确公开与非一致性范围的频道。 例如，低音信道都可能具有不同于其他渠道的范围。

下面的代码示例演示如何处理[音频属性的基本支持查询](basic-support-queries-for-audio-properties.md)使用非一致性的属性值。 点到下面的代码的第一行中的变量 pDescription [ **KSPROPERTY\_说明**](https://msdn.microsoft.com/library/windows/hardware/ff565132)的处理程序写入到其中的数据缓冲区开头的结构basic 支持的信息：

```cpp
  //
  // Fill in the members header.
  //
  PKSPROPERTY_MEMBERSHEADER pMembers = PKSPROPERTY_MEMBERSHEADER(pDescription + 1);

  pMembers->MembersFlags = KSPROPERTY_MEMBER_STEPPEDRANGES;
  pMembers->MembersSize = sizeof(KSPROPERTY_STEPPING_LONG);
  pMembers->MembersCount = ulNumChannels;
  pMembers->Flags = KSPROPERTY_MEMBER_FLAG_BASICSUPPORT_MULTICHANNEL;

  //
  // Fill in the stepped range with the driver default.
  //
  PKSPROPERTY_STEPPING_LONG pRange = PKSPROPERTY_STEPPING_LONG(pMembers + 1);
  pRange->Reserved = 0;

  for (ULONG i=0; i<ulNumChannels; i++)
  {
      pRange[i].Bounds.SignedMinimum = ulChannelMin[i];
      pRange[i].Bounds.SignedMaximum = ulChannelMax[i];
      pRange[i].SteppingDelta = ChannelStepping[i];
  }

  pPropertyRequest->ValueSize = sizeof(KSPROPERTY_DESCRIPTION) +
                                sizeof(KSPROPERTY_MEMBERSHEADER) + 
                                ulNumChannels * sizeof(KSPROPERTY_STEPPING_LONG);
```

下图显示了此示例中的数据缓冲区的布局。 PDescription、 pMembers 和 pRange 指针会显示指向缓冲区中它们各自的偏移量。

![说明的 basic 支持查询的数据缓冲区布局的关系图](images/propdesc.png)

对于此示例中，该处理程序设置**MembersCount**到**ulNumChannels**，通道数。 以字节为单位的范围数组大小

**MembersSize** \* **MembersCount**

请注意，如果 KSPROPERTY\_成员\_标志\_BASICSUPPORT\_统一标志已设置在此示例中，该处理程序会设置所有 KSPROPERTY\_单步执行\_中长时间结构到相同的范围的数组。

音节点的基本支持处理程序[ **KSPROPERTY\_音频\_低音**](https://msdn.microsoft.com/library/windows/hardware/ff537242)， [ **KSPROPERTY\_音频\_高音**](https://msdn.microsoft.com/library/windows/hardware/ff537308)，或[ **KSPROPERTY\_音频\_MID** ](https://msdn.microsoft.com/library/windows/hardware/ff537290)属性操作中类似的方式。

多渠道节点是否具有类型 BOOL 的每个通道属性值的属性，basic 支持处理程序必须填写有关单步执行范围数组的值。 在这种情况下，该处理程序中后面的代码示例所示的值设置的成员。 此类型的属性的两个示例都[ **KSPROPERTY\_音频\_设为静音**](https://msdn.microsoft.com/library/windows/hardware/ff537293)静音节点的属性和[ **KSPROPERTY\_音频\_低音\_BOOST** ](https://msdn.microsoft.com/library/windows/hardware/ff537245)音节点的属性。

下面的代码示例演示如何处理多渠道的节点，在具有类型 BOOL 的每个通道属性值的属性的情况下该 basic 支持请求：

```cpp
  //
  // Fill in the members header.
  //
  PKSPROPERTY_MEMBERSHEADER pMembers = PKSPROPERTY_MEMBERSHEADER(pDescription + 1);

  pMembers->MembersFlags = KSPROPERTY_MEMBER_STEPPEDRANGES;
  pMembers->MembersSize = sizeof (KSPROPERTY_STEPPING_LONG);
  pMembers->MembersCount = ulNumChannels;
  pMembers->Flags = KSPROPERTY_MEMBER_FLAG_BASICSUPPORT_MULTICHANNEL;

  pPropertyRequest->ValueSize = sizeof(KSPROPERTY_DESCRIPTION) +
                                sizeof(KSPROPERTY_MEMBERSHEADER) + 
                                ulNumChannels * sizeof(KSPROPERTY_STEPPING_LONG);

  //
  // Fill in the stepped range with values in FOR loop.
  //
  PKSPROPERTY_STEPPING_LONG pRange = PKSPROPERTY_STEPPING_LONG(pMembers + 1);
  pRange->Reserved = 0;

  for (ULONG i=0; i<ulNumChannels; i++)
  {
      pRange[i].Bounds.SignedMinimum = 0;
      pRange[i].Bounds.SignedMaximum = 1;
      pRange[i].SteppingDelta = 1;
  }
```

请注意，在前面的代码示例中，FOR 循环使用零 (0) 和一 （1） 若要设置的每个通道范围的最小值和最大值。 这是因为我们每个通道属性值为类型 BOOL 配置多渠道的节点。

如果统一的信道属性，可以 KSPROPERTY 之间执行位或运算\_成员\_标志\_BASICSUPPORT\_统一标志和 KSPROPERTY\_成员\_标志\_BASICSUPPORT\_多渠道标志并将结果分配给 pMembers-&gt;标记成员。 此值用于指示，硬件适用相同的属性值统一跨节点中的所有信道。

使用 KSPROPERTY\_成员\_标志\_平均和 KSPROPERTY\_成员\_标志\_多渠道标志消除了需要为对组频道，并公开一个单独通道，就像在 Ac97 示例驱动程序 Windows Driver Kit (WDK) 中的每个对立体声卷节点。 由于 Windows 版本之前比 Windows XP 不支持这些标志，必须使用您的驱动程序的基本支持处理程序[IPortClsVersion](https://msdn.microsoft.com/library/windows/hardware/ff536877)接口查询以便确定是否使用 Portcls.sys 版本这些标志。

拓扑分析器 (内核模式下[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)，Wdmaud.sys) 从其 WDM 音频驱动程序获取音频设备的拓扑。 分析器公开该设备为传统 mixer 设备通过旧的 Windows 多媒体**mixer** API。 在 Windows XP 及更高版本，WDMAud 使用 KSPROPERTY\_成员\_标志\_BASICSUPPORT\_多渠道标志以确定对报表中的通道数**cChannels**MIXERLINE 结构的成员。 此外，如果该节点的基本支持处理程序指定 KSPROPERTY\_成员\_标志\_BASICSUPPORT\_统一标志 WDMAud 设置 MIXERCONTROL\_CONTROLF\_将统一相应 MIXERCONTROL 结构中的标志。 通过此标志，应用程序可以确定是否它们可单独调整每个通道或统一通过主控件的所有通道。 MIXERCONTROL，MIXERLINE，有关详细信息和**mixer** API，请参阅 Microsoft Windows SDK 文档。

在 Windows XP 及更高版本，SndVol32 音量控制程序 (请参阅[任务栏和 SndVol32](systray-and-sndvol32.md)) 显示控件的多渠道的设备，如下图中所示。

![sndvol32 音量控制对话框的屏幕截图 ](images/volctrl.png)

如果 SndVol32 检测到具有两个以上声道的线条，它将替换正常平移控件标记为一个按钮**扬声器音量**，其显示在上图中的主音量滑块上方。 单击**扬声器音量**按钮会弹出一个对话框，显示某一特定行的通道的所有控件，如下图中所示。

![具有高级音频属性对话框中的扬声器音量的屏幕截图](images/spkrvol.png)

因为**mixer** API 公开频道号、 推断中当前所选的扬声器配置通道名称**高级音频属性**Windows 中的对话框多媒体控制面板 (Mmsys.cpl)。

例如，如果设备公开四个通道在行上的，并且用户已经选择了"四声道扬声器"，通道名称将是"Left"（通道 0）、"Right"（通道 1）、"返回"（通道 2），左右"返回"（通道 3），因为在上图中所示。 更改为"环绕音响扬声器"扬声器配置将导致"Left"（通道 0）、"Right"（通道 1）、"前端 Center"（通道 2） 和"返回 Center"（通道 3） 的通道映射。

在驱动程序级别，KSPROPERTY\_音频\_通道\_CONFIG 属性使用的掩码值为 KSAUDIO\_演讲者\_四核或 KSAUDIO\_演讲者\_到环绕分别表示四声道或外侧代码演讲者配置。 标头文件 Ksmedia.h 定义这些值，如下所示：

```cpp
  #define KSAUDIO_SPEAKER_QUAD      (SPEAKER_FRONT_LEFT | SPEAKER_FRONT_RIGHT | \
                                     SPEAKER_BACK_LEFT | SPEAKER_BACK_RIGHT)

  #define KSAUDIO_SPEAKER_SURROUND  (SPEAKER_FRONT_LEFT | SPEAKER_FRONT_RIGHT | \
                                     SPEAKER_FRONT_CENTER | SPEAKER_BACK_CENTER)
```

任一掩码包含四个指定的四个通道扬声器位置的位。 在任一情况下，KSPROPERTY\_音频\_VOLUMELEVEL 属性分别标识作为频道 0、 1、 2 和 3，这些相同的四个通道。

如果该节点的基本支持处理程序将设置 KSPROPERTY\_成员\_标志\_BASICSUPPORT\_统一标志位，滑块中所示**扬声器音量**更多信息的对话框中移动使用与任何单个滑块所做的更改。

 

 




