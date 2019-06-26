---
title: 声明旧资源
description: 声明旧资源
ms.assetid: f3e573a1-0e7a-422b-8bed-db3ba7712a2f
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，旧的资源
- 旧资源 WDK 视频微型端口
- 微型端口驱动程序 WDK Windows 2000 中，初始化
- 初始化微型端口驱动程序
- VIDEO_HW_INITIALIZATION_DATA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f5fa4670dee6cd357783448429fe79edd46e1b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370707"
---
# <a name="claiming-legacy-resources"></a>声明旧资源


## <span id="ddk_claiming_legacy_resources_gg"></span><span id="DDK_CLAIMING_LEGACY_RESOURCES_GG"></span>


微型端口驱动程序必须声明并报告中的所有旧资源及其[**视频\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)在驱动程序初始化过程中的结构. 旧资源是设备的 PCI 配置空间中未列出这些资源但的解码设备。 电源管理和停靠在遇到此部分中所述的方式不会报告的旧的资源时，将禁用基于 NT 的操作系统。

微型端口驱动程序必须执行以下操作以报告此类的旧的资源：

- 如果旧的资源列表中在编译时已知的设备填充以下两个字段的[**视频\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)结构，它是创建和初始化[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)例程：

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">结构成员</th>
  <th align="left">定义</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p><strong>HwLegacyResourceList</strong></p></td>
  <td align="left"><p>指向数组<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_access_range" data-raw-source="[&lt;strong&gt;VIDEO_ACCESS_RANGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_access_range)"> <strong>VIDEO_ACCESS_RANGE</strong> </a>结构。 每个结构描述设备 I/O 端口或 PCI 配置空间中未列出的视频适配器的内存范围。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><strong>HwLegacyResourceCount</strong></p></td>
  <td align="left"><p>是，数组中的元素数目<strong>HwLegacyResourceList</strong>点。</p></td>
  </tr>
  </tbody>
  </table>

     

<!-- -->

-   如果在编译时不知道旧的设备的资源列表，实现[ *HwVidLegacyResources* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_legacyresources)函数，并初始化**HwGetLegacyResources**视频的成员\_HW\_初始化\_数据以指向此函数。 例如，支持使用不同的旧资源组的两个设备的微型端口驱动程序将实现*HwVidLegacyResources*若要在运行时报告的旧的资源。 视频端口驱动程序将忽略**HwLegacyResourceList**并**HwLegacyResourceCount**视频成员\_HW\_初始化\_数据时微型端口驱动程序实现*HwVidLegacyResources*。

-   填写**RangePassive**字段中为每个视频\_访问\_相应地微型端口驱动程序中定义的范围结构。 设置**RangePassive**视频\_范围\_被动\_解码指示区域进行解码的硬件，但显示和视频微型端口驱动程序将永远不会接触它。 设置**RangePassive**视频\_范围\_10\_位\_解码指示设备解码十位区域的端口地址。

同样，驱动程序只应包括硬件解码但 PCI 不会占用的资源。 代码中的驱动程序，需要声明最小的旧的资源可能看起来如下所示：

```cpp
//              RangeStart        RangeLength
//              |                 |      RangeInIoSpace
//              |                 |      |  RangeVisible
//        +-----+-----+           |      |  |  RangeShareable
//       low         high         |      |  |  |  RangePassive
//        v           v           v      v  v  v  v
VIDEO_ACCESS_RANGE AccessRanges[] = {
    // [0] (0x3b0-0x3bb)
    {0x000003b0, 0x00000000, 0x0000000c, 1, 1, 1, 0},
    // [1] (0x3c0-0x3df)
    {0x000003C0, 0x00000000, 0x00000010, 1, 1, 1, 0},
    // [2] (0xa0000-0xaffff)
    {0x000A0000, 0x00000000, 0x00010000, 1, 0, 0, 0},
};
 
// Within the DriverEntry routine:
VIDEO_HW_INITIALIZATION_DATA hwInitData;
hwInitData.HwLegacyResourceList = AccessRanges;
hwInitData.HwLegacyResourceCount = 3;
```

微型端口驱动程序可以"回收"旧资源到后续调用中再次[ **VideoPortVerifyAccessRanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportverifyaccessranges); 但是，视频端口驱动程序将直接忽略请求针对任何以前已声明的资源。 如果尝试声明中的旧的访问范围微型端口驱动程序将在系统中禁用电源管理和停靠**VideoPortVerifyAccessRanges** ，不以前认领中**HwLegacyResourceList**期间[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)或在中返回*LegacyResourceList*参数[ *HwVidLegacyResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_legacyresources)。

 

 





