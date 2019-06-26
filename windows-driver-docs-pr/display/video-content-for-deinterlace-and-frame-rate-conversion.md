---
title: 要进行反交错和帧速率转换的视频内容
description: 要进行反交错和帧速率转换的视频内容
ms.assetid: 627b394e-c2e1-4327-adaa-0c3436ba3d1a
keywords:
- 去隔行 WDK DirectX VA，接收到的视频内容
- 帧速率转换 WDK DirectX VA
- 接收到 WDK DirectX VA 的视频内容
- 去隔行 WDK DirectX VA 的视频内容
- 视频内容的帧速率转换 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b78289f0d4a0b821b9436aa9005703df3939699
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365079"
---
# <a name="video-content-for-deinterlace-and-frame-rate-conversion"></a>要进行反交错和帧速率转换的视频内容


## <span id="ddk_video_content_for_deinterlace_and_frame_rate_conversion_gg"></span><span id="DDK_VIDEO_CONTENT_FOR_DEINTERLACE_AND_FRAME_RATE_CONVERSION_GG"></span>


驱动程序收到视频内容的说明，以便它可以确定如何它应取消隔行扫描或帧速率转换此类内容。 驱动程序收到此视频的内容作为一个指向[ **DXVA\_VideoDesc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)以下函数调用中的结构：

-   [**DeinterlaceQueryAvailableModes**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes)

-   [**DeinterlaceQueryModeCaps**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)

-   [**DeinterlaceOpenStream**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceopenstream)

下面的示例指示驱动程序上接收到的视频内容执行取消隔行和帧速率转换的方式。

### <a name="span-iddeinterlacing720x480icontentexamplespanspan-iddeinterlacing720x480icontentexamplespanspan-iddeinterlacing720x480icontentexamplespandeinterlacing-720-x-480i-content-example"></a><span id="Deinterlacing_720_x_480i_Content_Example"></span><span id="deinterlacing_720_x_480i_content_example"></span><span id="DEINTERLACING_720_X_480I_CONTENT_EXAMPLE"></span>取消隔行扫描 720 x 480i 内容示例

DXVA\_VideoDesc 结构，如下所示填充，指示要取消隔行扫描 720 x 480i 内容、 数据源作为每个样本 29.97 Hz 的频率的两个字段的驱动程序。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">值</th>
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
<td align="left"><p><strong>DXVA_SampleFieldInterleavedOddFirst</strong>中的枚举器<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ne-dxva-_dxva_sampleformat" data-raw-source="[&lt;strong&gt;DXVA_SampleFormat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ne-dxva-_dxva_sampleformat)"> <strong>DXVA_SampleFormat</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>d3dFormat</strong></p></td>
<td align="left"><p>在中定义 D3DFMT_YUY2 <em>d3d8types.h</em>并<em>d3d9types.h</em>标头文件</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>InputSampleFreq.Numerator</strong></p></td>
<td align="left"><p>30000 （29.97 Hz 监视器频率）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>InputSampleFreq.Denominator</strong></p></td>
<td align="left"><p>1001</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>OutputFrameFreq.Numerator</strong></p></td>
<td align="left"><p>60000 （59.94 Hz 监视器频率）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OutputFrameFreq.Denominator</strong></p></td>
<td align="left"><p>1001</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddeinterlacingandframe-rateconversionof720x480icontentexamplespanspan-iddeinterlacingandframe-rateconversionof720x480icontentexamplespanspan-iddeinterlacingandframe-rateconversionof720x480icontentexamplespandeinterlacing-and-frame-rate-conversion-of-720-x-480i-content-example"></a><span id="Deinterlacing_and_Frame-Rate_Conversion_of_720_x_480i_Content_Example"></span><span id="deinterlacing_and_frame-rate_conversion_of_720_x_480i_content_example"></span><span id="DEINTERLACING_AND_FRAME-RATE_CONVERSION_OF_720_X_480I_CONTENT_EXAMPLE"></span>取消隔行和 720 x 480i 内容示例的帧速率转换

**OutputFrameFreq** DXVA 成员\_VideoDesc 结构，如下所示填充，若要指示驱动程序来取消隔行扫描和帧速率转换 720 x 480i 内容。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>OutputFrameFreq.Numerator</strong></p></td>
<td align="left"><p>85 （85 Hz 监视器频率）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OutputFrameFreq.Denominator</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddeinterlacingasinglefieldtoaprogressiveframeexamplespanspan-iddeinterlacingasinglefieldtoaprogressiveframeexamplespanspan-iddeinterlacingasinglefieldtoaprogressiveframeexamplespandeinterlacing-a-single-field-to-a-progressive-frame-example"></a><span id="Deinterlacing_a_Single_Field_to_a_Progressive_Frame_Example"></span><span id="deinterlacing_a_single_field_to_a_progressive_frame_example"></span><span id="DEINTERLACING_A_SINGLE_FIELD_TO_A_PROGRESSIVE_FRAME_EXAMPLE"></span>去隔行单个字段以渐进式帧示例

**OutputFrameFreq** DXVA 成员\_VideoDesc 结构，如下所示填充，若要指示驱动程序来取消隔行扫描到更高版本的 MPEG 编码渐进式帧的单个字段。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>OutputFrameFreq.Numerator</strong></p></td>
<td align="left"><p>30000 （29.97 Hz 监视器频率）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OutputFrameFreq.Denominator</strong></p></td>
<td align="left"><p>1001</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idframe-rateconversionof480pcontentexamplespanspan-idframe-rateconversionof480pcontentexamplespanspan-idframe-rateconversionof480pcontentexamplespanframe-rate-conversion-of-480p-content-example"></a><span id="Frame-Rate_Conversion_of__480p_Content_Example"></span><span id="frame-rate_conversion_of__480p_content_example"></span><span id="FRAME-RATE_CONVERSION_OF__480P_CONTENT_EXAMPLE"></span>480p 内容示例的帧速率转换

DXVA\_VideoDesc 结构填充如下所示，若要指示驱动程序可执行帧速率转换 480p 的内容并与匹配监视器显示频率。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">ReplTest1</th>
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
<td align="left"><p><strong>DXVA_SampleProgressiveFrame</strong>中的枚举器<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ne-dxva-_dxva_sampleformat" data-raw-source="[&lt;strong&gt;DXVA_SampleFormat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ne-dxva-_dxva_sampleformat)"> <strong>DXVA_SampleFormat</strong> </a>枚举</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>d3dFormat</strong></p></td>
<td align="left"><p>D3DFMT_YUY2 d3d8types.h 和 d3d9types.h 标头文件中定义</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>InputSampleFreq.Numerator</strong></p></td>
<td align="left"><p>60 （60 Hz 监视器频率）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>InputSampleFreq.Denominator</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>OutputFrameFreq.Numerator</strong></p></td>
<td align="left"><p>85 （85 Hz 监视器频率）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OutputFrameFreq.Denominator</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

 

 





