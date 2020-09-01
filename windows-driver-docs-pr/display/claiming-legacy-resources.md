---
title: 声明旧资源
description: 声明旧资源
ms.assetid: f3e573a1-0e7a-422b-8bed-db3ba7712a2f
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，旧版资源
- 旧资源 WDK 视频微型端口
- 视频微型端口驱动程序 WDK Windows 2000，初始化
- 初始化视频微型端口驱动程序
- VIDEO_HW_INITIALIZATION_DATA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c792c58e044bee09eb269b1441b47f228f0243fe
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065682"
---
# <a name="claiming-legacy-resources"></a>声明旧资源


## <span id="ddk_claiming_legacy_resources_gg"></span><span id="DDK_CLAIMING_LEGACY_RESOURCES_GG"></span>


在驱动程序初始化期间，视频微型端口驱动程序必须声明并报告其 [**视频 \_ HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data) 结构中的所有旧资源。 旧资源是指未列出在设备 PCI 配置空间中的资源，但被设备解码。 基于 NT 的操作系统会在遇到此部分中所述的情况下，禁用未报告的旧资源。

微型端口驱动程序必须执行以下操作来报告此类旧资源：

- 如果设备的旧版资源列表在编译时已知，请在[**DriverEntry**](./driverentry-of-video-miniport-driver.md)例程中填写创建和初始化的[**视频 \_ HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)结构的以下两个字段：

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
  <td align="left"><p>指向 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_access_range" data-raw-source="[&lt;strong&gt;VIDEO_ACCESS_RANGE&lt;/strong&gt;](/windows-hardware/drivers/ddi/video/ns-video-_video_access_range)"><strong>VIDEO_ACCESS_RANGE</strong></a> 结构的数组。 每个结构都描述了 PCI 配置空间中未列出的视频适配器的设备 i/o 端口或内存范围。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><strong>HwLegacyResourceCount</strong></p></td>
  <td align="left"><p><strong>HwLegacyResourceList</strong>指向的数组中的元素数。</p></td>
  </tr>
  </tbody>
  </table>

     

<!-- -->

-   如果在编译时设备的旧资源列表未知，则实现 [*HwVidLegacyResources*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_legacyresources) 函数，并将视频 HW 初始化数据的 **HwGetLegacyResources** 成员初始化 \_ \_ \_ 为指向此函数。 例如，如果某个微型端口驱动程序支持具有不同的旧式资源集的两个设备，则会在运行时实现 *HwVidLegacyResources* 来报告旧资源。 **HwLegacyResourceList** **HwLegacyResourceCount** \_ \_ \_ 当微型端口驱动程序实现*HwVidLegacyResources*时，视频端口驱动程序将忽略视频 HW 初始化数据的 HwLegacyResourceList 和 HwLegacyResourceCount 成员。

-   为**RangePassive** \_ \_ 微型端口驱动程序中定义的每个视频访问范围结构填写 "RangePassive" 字段。 将 **RangePassive** 设置为视频 \_ 范围 \_ 被动 \_ 解码表示该区域由硬件解码，但显示器和视频微型端口驱动程序将永远不会接触到该区域。 将 **RangePassive** 设置为视频 \_ 范围为 \_ 10 \_ 位 \_ 解码表示设备对区域的端口地址的10位进行解码。

同样，驱动程序应该只包含硬件解码但不由 PCI 声明的资源。 需要声明最少旧资源的驱动程序中的代码可能如下所示：

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

小型端口驱动程序可以在后续 (调用中再次 "回收" 旧资源) [**VideoPortVerifyAccessRanges**](/windows-hardware/drivers/ddi/video/nf-video-videoportverifyaccessranges);但是，视频端口驱动程序将忽略对以前声明的任何资源的请求。 如果微型端口驱动程序尝试在**VideoPortVerifyAccessRanges** [**中声明**](./driverentry-of-video-miniport-driver.md)以前未在**HwLegacyResourceList**期间声明的旧访问范围，或在[*HwVidLegacyResources*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_legacyresources)的*LegacyResourceList*参数中返回，则系统将禁用电源管理和停靠。

 

