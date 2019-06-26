---
title: DriverEntry 的视频微型端口驱动程序函数
description: DriverEntry 是视频的微型端口驱动程序的初始入口点。
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
ms.openlocfilehash: e1ea2aa1be31527e253ff2a17e3455f15a271878
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384268"
---
# <a name="driverentry-of-video-miniport-driver-function"></a>DriverEntry 的视频微型端口驱动程序函数


**DriverEntry**是视频的微型端口驱动程序的初始入口点。

<a name="syntax"></a>语法
------

```cpp
ULONG DriverEntry(
  _In_ PVOID Context1,
  _In_ PVOID Context2
);
```

<a name="parameters"></a>Parameters
----------

*Context1* \[中\]微型端口驱动程序必须与其调用的上下文值指向[ **VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportinitialize)。 此上下文值标识创建为此微型端口驱动程序的系统的驱动程序对象。

*Context2* \[中\]微型端口驱动程序必须与其调用的第二个上下文值指向[ **VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportinitialize)。 此上下文值标识此微型端口驱动程序的注册表路径。

<a name="return-value"></a>返回值
------------

**DriverEntry**返回的值将返回[ **VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportinitialize)。

<a name="remarks"></a>备注
-------

每个微型端口驱动程序必须具有显式命名的函数**DriverEntry**才能加载。 **DriverEntry**由 I/O 系统直接调用。

**DriverEntry**必须执行以下步骤：

-   在堆栈上分配内存[**视频\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)结构，并调用[ **VideoPortZeroMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportzeromemory)以零初始化。

-   在视频中的特定于驱动程序和特定于适配器的值填充\_HW\_初始化\_数据成员，包括微型端口驱动程序的入口点。 以下入口点必须设置为微型端口驱动程序提供的例程：

    [*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)

    [*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_initialize)

    [*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_start_io)

    [*HwVidInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_interrupt)

    [*HwVidQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_query_interface)

    [*HwVidGetVideoChildDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_get_child_descriptor)

    [*HwVidGetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_power_get)

    [*HwVidSetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_power_set)

-   如果驱动程序的硬件支持的旧的资源，该驱动程序必须报告它们。 **DriverEntry**应该执行以下，如果在驱动程序编译时已知的资源列表：

    -   声明和报告中的所有此类资源**HwLegacyResourceList**并**HwLegacyResourceCount**的成员[**视频\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)结构。 旧资源是设备的 PCI 配置空间中未列出这些资源但的解码设备。
    -   填写**RangePassive**相应地字段为每个[**视频\_访问\_范围**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_access_range)微型端口驱动程序中定义的结构。

    如果旧的资源列表不能确定运行时之前，该驱动程序应改为实现[ *HwVidLegacyResources* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_legacyresources)函数进行报告。

-   调用[ **VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportinitialize)，并传递*Context1*并*Context2*作为前两个参数，指向视频\_HW\_初始化\_的第三个参数的数据结构和**NULL**作为第四个参数。

**DriverEntry**返回的值应传播[ **VideoPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportinitialize)回调用方。

如果**DriverEntry** does 声明资源，它应包括硬件解码，但的未声明的 PCI 的资源。 微型端口驱动程序可以"回收"这些旧资源到后续调用中再次[ **VideoPortVerifyAccessRanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportverifyaccessranges); 但是，视频端口驱动程序将直接忽略请求的任何此类以前已声明的资源。 如果尝试声明中的旧的访问范围微型端口驱动程序将在系统中禁用电源管理和停靠**VideoPortVerifyAccessRanges** ，不以前认领中**HwLegacyResourceList**的成员[**视频\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)结构期间**DriverEntry**(或在[ *HwVidLegacyResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_legacyresources)，如果实现)。

有关 Microsoft Windows 2000 和更高版本还支持运行 Windows NT 4.0 的计算机的驱动程序，硬件配置常量中定义*video.h*。 这些常量以下表所述。

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
<td align="left"><p>大小 （字节） Windows NT 4.0 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_port_config_info" data-raw-source="[&lt;strong&gt;VIDEO_PORT_CONFIG_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_port_config_info)"> <strong>VIDEO_PORT_CONFIG_INFO</strong> </a>结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SIZE_OF_NT4_VIDEO_HW_INITIALIZATION_DATA</p></td>
<td align="left"><p>大小 （字节） Windows NT 4.0 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data" data-raw-source="[&lt;strong&gt;VIDEO_HW_INITIALIZATION_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)"> <strong>VIDEO_HW_INITIALIZATION_DATA</strong> </a>结构。 如果<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportinitialize" data-raw-source="[&lt;strong&gt;VideoPortInitialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportinitialize)"> <strong>VideoPortInitialize</strong> </a>失败，微型端口驱动程序应将设置<strong>HwInitDataSize</strong> VIDEO_HW_INITIALIZATION_DATA 结构的大小中的成员此结构的 Windows 2000 （和更高版本） 版本或 Windows NT 4.0 版本。 选择适当的结构大小以匹配微型端口驱动程序将在其中运行的操作系统版本。 然后应调用微型端口驱动程序<strong>VideoPortInitialize</strong>试。 使用的示例，请参阅 Windows 驱动程序开发工具包 (DDK) 中包含的微型端口驱动程序示例。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SIZE_OF_W2K_VIDEO_HW_INITIALIZATION_DATA</p></td>
<td align="left"><p>大小 （字节），Windows 2000 及更高版本<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data" data-raw-source="[&lt;strong&gt;VIDEO_HW_INITIALIZATION_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)"> <strong>VIDEO_HW_INITIALIZATION_DATA</strong> </a>结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SIZE_OF_WXP_VIDEO_HW_INITIALIZATION_DATA</p></td>
<td align="left"><p>大小 （字节），Windows Vista 及更高版本<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data" data-raw-source="[&lt;strong&gt;VIDEO_HW_INITIALIZATION_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)"> <strong>VIDEO_HW_INITIALIZATION_DATA</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SIZE_OF_WXP_VIDEO_PORT_CONFIG_INFO</p></td>
<td align="left"><p>大小 （字节），Windows Vista <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_port_config_info" data-raw-source="[&lt;strong&gt;VIDEO_PORT_CONFIG_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_port_config_info)"> <strong>VIDEO_PORT_CONFIG_INFO</strong> </a>结构。</p></td>
</tr>
</tbody>
</table>

 

**DriverEntry**应进行可分页。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Video.h （包括 Video.h）</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">NtosKrnl.lib</td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)

[*HwVidLegacyResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_legacyresources)

[**VIDEO\_HW\_INITIALIZATION\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)

[**VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportinitialize)

[**VideoPortVerifyAccessRanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportverifyaccessranges)

[**VideoPortZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportzeromemory)

 

 






