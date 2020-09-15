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
ms.openlocfilehash: e0ff4dde8e05098f40d0e68e822327e4689295e5
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103788"
---
# <a name="driverentry-of-video-miniport-driver-function"></a>视频微型端口驱动程序函数的 DriverEntry


**DriverEntry** 是视频微型端口驱动程序的初始入口点。

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

*Context1* \[指向 \] 一个上下文值的指针，微型端口驱动程序必须调用 [**VideoPortInitialize**](/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)。 此上下文值标识系统为此微型端口驱动程序创建的驱动程序对象。

*Context2* \[指向 \] 第二个上下文值的指针，微型端口驱动程序必须在此值中调用 [**VideoPortInitialize**](/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)。 此上下文值标识此微型端口驱动程序的注册表路径。

<a name="return-value"></a>返回值
------------

**DriverEntry** 返回 [**VideoPortInitialize**](/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)返回的值。

<a name="remarks"></a>注解
-------

每个微型端口驱动程序必须具有显式命名为 **DriverEntry** 的函数才能加载。 **DriverEntry** 是由 i/o 系统直接调用的。

**DriverEntry** 必须执行以下步骤：

-   为 [**视频 \_ HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data) 结构在堆栈上分配内存，并调用 [**VideoPortZeroMemory**](/windows-hardware/drivers/ddi/video/nf-video-videoportzeromemory) 将其初始化为零。

-   在视频 \_ HW \_ 初始化 \_ 数据成员（包括微型端口驱动程序的入口点）中填写驱动程序特定和特定于适配器的值。 以下入口点必须设置为微型端口驱动程序提供的例程：

    [*HwVidFindAdapter*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)

    [*HwVidInitialize*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize)

    [*HwVidStartIO*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)

    [*HwVidInterrupt*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_interrupt)

    [*HwVidQueryInterface*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_query_interface)

    [*HwVidGetVideoChildDescriptor*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_get_child_descriptor)

    [*HwVidGetPowerState*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_power_get)

    [*HwVidSetPowerState*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_power_set)

-   如果驱动程序的硬件支持旧版资源，则驱动程序必须对其进行报告。 如果资源列表在驱动程序编译时是已知的，则**DriverEntry**应执行以下操作：

    -   在[**视频 \_ HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)结构的**HwLegacyResourceList**和**HwLegacyResourceCount**成员中声明和报告所有此类资源。 旧资源是指未列出在设备 PCI 配置空间中的资源，但被设备解码。
    -   为微型端口驱动程序中定义的每个[**视频 \_ 访问 \_ 范围**](/windows-hardware/drivers/ddi/video/ns-video-_video_access_range)结构填写 " **RangePassive** " 字段。

    如果在运行时之前无法确定旧资源列表，则驱动程序应改为实现 [*HwVidLegacyResources*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_legacyresources) 函数来报告它们。

-   调用 [**VideoPortInitialize**](/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)，将 *Context1* 和 *Context2* 传递为前两个参数，将和作为第三个参数传递到视频 \_ HW \_ 初始化 \_ 数据结构，并将 **NULL** 作为第四个参数。

**DriverEntry** 应将 [**VideoPortInitialize**](/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize) 返回的值传播回调用方。

如果 **DriverEntry** 确实声明资源，则它应仅包含硬件解码但不是 PCI 声明的那些资源。 小型端口驱动程序可以在后续 (调用中再次 "回收" 这些旧资源) [**VideoPortVerifyAccessRanges**](/windows-hardware/drivers/ddi/video/nf-video-videoportverifyaccessranges);但是，视频端口驱动程序将忽略对以前声明的任何资源的请求。 如果微型端口驱动程序尝试在**VideoPortVerifyAccessRanges**中声明以前未在**DriverEntry** (或[*HwVidLegacyResources*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_legacyresources)中**声明的旧**访问范围（如果实现了) ），则将在系统中禁用电源管理和停靠。 [** \_ \_ \_ **](/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)

对于还支持运行 Windows NT 4.0 的计算机的 Microsoft Windows 2000 及更高版本的驱动程序，硬件配置常量在 *video*中定义。 下表描述了这些常量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回的常量</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SIZE_OF_NT4_VIDEO_PORT_CONFIG_INFO</p></td>
<td align="left"><p>Windows NT 4.0 <a href="/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info" data-raw-source="[&lt;strong&gt;VIDEO_PORT_CONFIG_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info)"><strong>VIDEO_PORT_CONFIG_INFO</strong></a> 结构的大小（以字节为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SIZE_OF_NT4_VIDEO_HW_INITIALIZATION_DATA</p></td>
<td align="left"><p>Windows NT 4.0 <a href="/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data" data-raw-source="[&lt;strong&gt;VIDEO_HW_INITIALIZATION_DATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)"><strong>VIDEO_HW_INITIALIZATION_DATA</strong></a> 结构的大小（以字节为单位）。 如果 <a href="/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize" data-raw-source="[&lt;strong&gt;VideoPortInitialize&lt;/strong&gt;](/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)"><strong>VideoPortInitialize</strong></a> 失败，则视频微型端口驱动程序应将 VIDEO_HW_INITIALIZATION_DATA 结构的 <strong>HwInitDataSize</strong> 成员设置为此结构或 windows NT 4.0 版本的 windows 2000 (和更) 高版本的大小。 选择适当的结构大小，以匹配要运行微型端口驱动程序的操作系统版本。 然后，视频微型端口驱动程序应再次调用 <strong>VideoPortInitialize</strong> 。 有关使用的示例，请参阅 Windows 驱动程序开发工具包 (DDK) 中包含的视频微型端口驱动程序示例。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SIZE_OF_W2K_VIDEO_HW_INITIALIZATION_DATA</p></td>
<td align="left"><p>Windows 2000 和更高版本 <a href="/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data" data-raw-source="[&lt;strong&gt;VIDEO_HW_INITIALIZATION_DATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)"><strong>VIDEO_HW_INITIALIZATION_DATA</strong></a> 结构的大小（以字节为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SIZE_OF_WXP_VIDEO_HW_INITIALIZATION_DATA</p></td>
<td align="left"><p>Windows Vista 和更高版本 <a href="/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data" data-raw-source="[&lt;strong&gt;VIDEO_HW_INITIALIZATION_DATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)"><strong>VIDEO_HW_INITIALIZATION_DATA</strong></a> 结构的大小（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SIZE_OF_WXP_VIDEO_PORT_CONFIG_INFO</p></td>
<td align="left"><p>Windows Vista <a href="/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info" data-raw-source="[&lt;strong&gt;VIDEO_PORT_CONFIG_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info)"><strong>VIDEO_PORT_CONFIG_INFO</strong></a> 结构的大小（以字节为单位）。</p></td>
</tr>
</tbody>
</table>

 

**DriverEntry** 应进行分页。

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
<td align="left">桌面型</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Video (包含 Video) </td>
</tr>
<tr class="odd">
<td align="left"><p>库</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[*HwVidFindAdapter*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)

[*HwVidLegacyResources*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_legacyresources)

[**视频 \_ 硬件 \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)

[**VideoPortInitialize**](/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)

[**VideoPortVerifyAccessRanges**](/windows-hardware/drivers/ddi/video/nf-video-videoportverifyaccessranges)

[**VideoPortZeroMemory**](/windows-hardware/drivers/ddi/video/nf-video-videoportzeromemory)

