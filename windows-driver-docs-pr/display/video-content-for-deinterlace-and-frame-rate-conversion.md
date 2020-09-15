---
title: 要进行反交错和帧速率转换的视频内容
description: 要进行反交错和帧速率转换的视频内容
ms.assetid: 627b394e-c2e1-4327-adaa-0c3436ba3d1a
keywords:
- 取消隔行扫描 WDK DirectX VA，接收视频内容
- 帧速率转换 WDK DirectX VA
- 已收到视频内容 WDK DirectX VA
- 取消隔行扫描 WDK DirectX VA 视频内容
- 帧速率转换的视频内容 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91ef1c8aabe1b997f19612335da4b3d736137e44
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107524"
---
# <a name="video-content-for-deinterlace-and-frame-rate-conversion"></a>要进行反交错和帧速率转换的视频内容


## <span id="ddk_video_content_for_deinterlace_and_frame_rate_conversion_gg"></span><span id="DDK_VIDEO_CONTENT_FOR_DEINTERLACE_AND_FRAME_RATE_CONVERSION_GG"></span>


驱动程序接收视频内容的描述，以便它可以确定它应如何进行隔行扫描或帧速率转换此类内容。 驱动程序接收此视频内容，作为指向以下函数调用中的 [**DXVA \_ VideoDesc**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc) 结构的指针：

-   [**DeinterlaceQueryAvailableModes**](./dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)

-   [**DeinterlaceQueryModeCaps**](./dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps.md)

-   [**DeinterlaceOpenStream**](./dxva-deinterlacebobdeviceclass-deinterlaceopenstream.md)

以下示例说明了驱动程序如何对收到的视频内容执行取消隔行扫描和帧速率转换。

### <a name="span-iddeinterlacing_720_x_480i_content_examplespanspan-iddeinterlacing_720_x_480i_content_examplespanspan-iddeinterlacing_720_x_480i_content_examplespandeinterlacing-720-x-480i-content-example"></a><span id="Deinterlacing_720_x_480i_Content_Example"></span><span id="deinterlacing_720_x_480i_content_example"></span><span id="DEINTERLACING_720_X_480I_CONTENT_EXAMPLE"></span>取消隔行扫描 720 x 480i 内容示例

DXVA \_ VideoDesc 结构按如下方式进行填充，以将驱动程序定向到逐行 720 x 480i 内容中，以 29.97 Hz 的频率为每个样本发出两个字段。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>SampleWidth</strong></p></td>
<td align="left"><p>720</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SampleHeight</strong></p></td>
<td align="left"><p>480</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SampleFormat</strong></p></td>
<td align="left"><p>DXVA_SampleFormat 中的<strong>DXVA_SampleFieldInterleavedOddFirst</strong>枚举器<a href="/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_sampleformat" data-raw-source="[&lt;strong&gt;DXVA_SampleFormat&lt;/strong&gt;](/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_sampleformat)"> <strong>DXVA_SampleFormat</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>d3dFormat</strong></p></td>
<td align="left"><p><em>D3d8types</em>和<em>d3d9types</em>头文件中定义的 D3DFMT_YUY2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>InputSampleFreq</strong></p></td>
<td align="left"><p>30000 (29.97-Hz 监视器频率) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>InputSampleFreq</strong></p></td>
<td align="left"><p>1001</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>OutputFrameFreq</strong></p></td>
<td align="left"><p>60000 (59.94-Hz 监视器频率) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OutputFrameFreq</strong></p></td>
<td align="left"><p>1001</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddeinterlacing_and_frame-rate_conversion_of_720_x_480i_content_examplespanspan-iddeinterlacing_and_frame-rate_conversion_of_720_x_480i_content_examplespanspan-iddeinterlacing_and_frame-rate_conversion_of_720_x_480i_content_examplespandeinterlacing-and-frame-rate-conversion-of-720-x-480i-content-example"></a><span id="Deinterlacing_and_Frame-Rate_Conversion_of_720_x_480i_Content_Example"></span><span id="deinterlacing_and_frame-rate_conversion_of_720_x_480i_content_example"></span><span id="DEINTERLACING_AND_FRAME-RATE_CONVERSION_OF_720_X_480I_CONTENT_EXAMPLE"></span>720 x 480i 内容示例的取消隔行扫描和帧速率转换

DXVA VideoDesc 结构的 **OutputFrameFreq** 成员 \_ 按如下方式进行填充，以将驱动程序定向到隔行扫描和帧速率转换 720 x 480i 内容。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>OutputFrameFreq</strong></p></td>
<td align="left"><p>85 (85-Hz 监视器频率) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OutputFrameFreq</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddeinterlacing_a_single_field_to_a_progressive_frame_examplespanspan-iddeinterlacing_a_single_field_to_a_progressive_frame_examplespanspan-iddeinterlacing_a_single_field_to_a_progressive_frame_examplespandeinterlacing-a-single-field-to-a-progressive-frame-example"></a><span id="Deinterlacing_a_Single_Field_to_a_Progressive_Frame_Example"></span><span id="deinterlacing_a_single_field_to_a_progressive_frame_example"></span><span id="DEINTERLACING_A_SINGLE_FIELD_TO_A_PROGRESSIVE_FRAME_EXAMPLE"></span>将单个字段取消隔行扫描为渐进式帧示例

DXVA VideoDesc 结构的 **OutputFrameFreq** 成员 \_ 按如下方式进行填充，以指示驱动程序将单个字段逐行到渐进式帧以供以后使用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>OutputFrameFreq</strong></p></td>
<td align="left"><p>30000 (29.97-Hz 监视器频率) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OutputFrameFreq</strong></p></td>
<td align="left"><p>1001</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idframe-rate_conversion_of__480p_content_examplespanspan-idframe-rate_conversion_of__480p_content_examplespanspan-idframe-rate_conversion_of__480p_content_examplespanframe-rate-conversion-of-480p-content-example"></a><span id="Frame-Rate_Conversion_of__480p_Content_Example"></span><span id="frame-rate_conversion_of__480p_content_example"></span><span id="FRAME-RATE_CONVERSION_OF__480P_CONTENT_EXAMPLE"></span>480p 内容示例的帧速率转换

DXVA \_ VideoDesc 结构的填充方式如下，指示驱动程序对480p 内容执行帧速率转换，并与监视器显示频率匹配。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>SampleWidth</strong></p></td>
<td align="left"><p>720</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SampleHeight</strong></p></td>
<td align="left"><p>480</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SampleFormat</strong></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_sampleformat" data-raw-source="[&lt;strong&gt;DXVA_SampleFormat&lt;/strong&gt;](/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_sampleformat)"><strong>DXVA_SampleFormat</strong></a>枚举中的<strong>DXVA_SampleProgressiveFrame</strong>枚举器</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>d3dFormat</strong></p></td>
<td align="left"><p>D3d8types 和 d3d9types 头文件中定义的 D3DFMT_YUY2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>InputSampleFreq</strong></p></td>
<td align="left"><p>60 (60 Hz 监视器频率) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>InputSampleFreq</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>OutputFrameFreq</strong></p></td>
<td align="left"><p>85 (85 Hz 监视器频率) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OutputFrameFreq</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

