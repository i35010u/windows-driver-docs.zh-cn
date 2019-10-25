---
title: 视频微型端口驱动程序函数的 DriverEntry
description: DriverEntry 是视频微型端口驱动程序的初始入口点。
ms.assetid: b927dd2c-19e1-49bc-b30b-530efe2ba13b
keywords:
- DriverEntry 函数显示设备
topic_type:
- apiref
api_name:
- DriverEntry
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7c23d16c3f026ca09fea9efb2bf12cc080af26b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839732"
---
# <a name="driverentry-of-video-miniport-driver-function"></a>视频微型端口驱动程序函数的 DriverEntry


**DriverEntry**是视频微型端口驱动程序的初始入口点。

<a name="syntax"></a>语法
------

```cpp
ULONG DriverEntry(
  _In_ PVOID Context1,
  _In_ PVOID Context2
);
```

<a name="parameters"></a>参数
----------

*Context1* \[\] 指针指向一个上下文值，微型端口驱动程序必须在该上下文值中调用[**VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)。 此上下文值标识系统为此微型端口驱动程序创建的驱动程序对象。

*Context2* \[\] 指向第二个上下文值的指针，微型端口驱动程序必须调用[**VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)。 此上下文值标识此微型端口驱动程序的注册表路径。

<a name="return-value"></a>返回值
------------

**DriverEntry**返回[**VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)返回的值。

<a name="remarks"></a>备注
-------

每个微型端口驱动程序必须具有显式命名为**DriverEntry**的函数才能加载。 **DriverEntry**是由 i/o 系统直接调用的。

**DriverEntry**必须执行以下步骤：

-   在堆栈上分配内存[ **\_硬件\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)结构，并调用[**VideoPortZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportzeromemory)将其初始化为零。

-   在视频\_HW\_初始化\_数据成员（包括微型端口驱动程序的入口点）中填写驱动程序特定和特定于适配器的值。 以下入口点必须设置为微型端口驱动程序提供的例程：

    [*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)

    [*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize)

    [*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)

    [*HwVidInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_interrupt)

    [*HwVidQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_query_interface)

    [*HwVidGetVideoChildDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_get_child_descriptor)

    [*HwVidGetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_power_get)

    [*HwVidSetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_power_set)

-   如果驱动程序的硬件支持旧版资源，则驱动程序必须对其进行报告。 如果资源列表在驱动程序编译时是已知的，则**DriverEntry**应执行以下操作：

    -   在视频的**HwLegacyResourceList**和**HwLegacyResourceCount**成员中声明和报告所有此类资源[ **\_HW\_初始化\_的数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)结构。 旧资源是指未列出在设备 PCI 配置空间中的资源，但被设备解码。
    -   在 RangePassive 字段中，为每个视频填写相应的字段，\_访问在微型端口驱动程序中定义[ **\_范围**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_access_range)结构。

    如果在运行时之前无法确定旧资源列表，则驱动程序应改为实现[*HwVidLegacyResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_legacyresources)函数来报告它们。

-   调用[**VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)，将*Context1*和*Context2*作为前两个参数传递，指向视频\_硬件的指针\_初始化\_数据结构作为第三个参数，并将**NULL**作为第四个参数。参数.

**DriverEntry**应将[**VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)返回的值传播回调用方。

如果**DriverEntry**确实声明资源，则它应仅包含硬件解码但不是 PCI 声明的那些资源。 小型端口驱动程序可以在后续调用中再次 "回收" 这些旧资源到[**VideoPortVerifyAccessRanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportverifyaccessranges);但是，视频端口驱动程序将忽略对以前声明的任何资源的请求。 如果微型端口驱动程序尝试在**VideoPortVerifyAccessRanges**中声明以前未在视频的**HwLegacyResourceList**成员中声明的旧访问范围，将在系统中禁用电源管理和插接[ **\_HW\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)在**DriverEntry**期间（或者在[*HwVidLegacyResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_legacyresources)中实现）\_数据结构进行初始化。

对于还支持运行 Windows NT 4.0 的计算机的 Microsoft Windows 2000 及更高版本的驱动程序，硬件配置常量在*video*中定义。 下表描述了这些常量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Constant</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SIZE_OF_NT4_VIDEO_PORT_CONFIG_INFO</p></td>
<td align="left"><p>Windows NT 4.0 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info" data-raw-source="[&lt;strong&gt;VIDEO_PORT_CONFIG_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info)"><strong>VIDEO_PORT_CONFIG_INFO</strong></a>结构的大小（以字节为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SIZE_OF_NT4_VIDEO_HW_INITIALIZATION_DATA</p></td>
<td align="left"><p>Windows NT 4.0 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data" data-raw-source="[&lt;strong&gt;VIDEO_HW_INITIALIZATION_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)"><strong>VIDEO_HW_INITIALIZATION_DATA</strong></a>结构的大小（以字节为单位）。 如果<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize" data-raw-source="[&lt;strong&gt;VideoPortInitialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)"><strong>VideoPortInitialize</strong></a>失败，则视频微型端口驱动程序应将 VIDEO_HW_INITIALIZATION_DATA 结构的<strong>HwInitDataSize</strong>成员设置为此结构或 Windows NT 4.0 的 windows 2000 （和更高版本）的大小。版本。 选择适当的结构大小，以匹配要运行微型端口驱动程序的操作系统版本。 然后，视频微型端口驱动程序应再次调用<strong>VideoPortInitialize</strong> 。 有关使用的示例，请参阅 Windows 驱动程序开发工具包（DDK）中包含的视频微型端口驱动程序示例。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SIZE_OF_W2K_VIDEO_HW_INITIALIZATION_DATA</p></td>
<td align="left"><p>Windows 2000 和更高版本的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data" data-raw-source="[&lt;strong&gt;VIDEO_HW_INITIALIZATION_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)"><strong>VIDEO_HW_INITIALIZATION_DATA</strong></a>结构的大小（以字节为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SIZE_OF_WXP_VIDEO_HW_INITIALIZATION_DATA</p></td>
<td align="left"><p>Windows Vista 和更高版本的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data" data-raw-source="[&lt;strong&gt;VIDEO_HW_INITIALIZATION_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)"><strong>VIDEO_HW_INITIALIZATION_DATA</strong></a>结构的大小（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SIZE_OF_WXP_VIDEO_PORT_CONFIG_INFO</p></td>
<td align="left"><p>Windows Vista <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info" data-raw-source="[&lt;strong&gt;VIDEO_PORT_CONFIG_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info)"><strong>VIDEO_PORT_CONFIG_INFO</strong></a>结构的大小（以字节为单位）。</p></td>
</tr>
</tbody>
</table>

 

**DriverEntry**应进行分页。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Video （包括 Video）</td>
</tr>
<tr class="odd">
<td align="left"><p>库</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)

[*HwVidLegacyResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_legacyresources)

[**视频\_硬件\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)

[**VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)

[**VideoPortVerifyAccessRanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportverifyaccessranges)

[**VideoPortZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportzeromemory)

 

 






