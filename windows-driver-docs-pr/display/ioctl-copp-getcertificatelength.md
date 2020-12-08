---
title: IOCTL \_ COPP \_ GetCertificateLength 控制代码
description: 返回图形硬件使用的证书的大小（以字节为单位）。
keywords:
- IOCTL_COPP_GetCertificateLength 控制代码显示设备
topic_type:
- apiref
api_name:
- IOCTL_COPP_GetCertificateLength
api_type:
- NA
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7965c43adf11c473ecb9d03502358f08e62065d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832755"
---
# <a name="ioctl_copp_getcertificatelength-control-code"></a>IOCTL \_ COPP \_ GetCertificateLength 控制代码


返回图形硬件使用的证书的大小（以字节为单位）。

## <span id="ddk_ioctl_copp_getcertificatelength_gg"></span><span id="DDK_IOCTL_COPP_GETCERTIFICATELENGTH_GG"></span>


### <a name="span-idinput_parametersspanspan-idinput_parametersspanspan-idinput_parametersspaninput-parameters"></a><span id="Input_Parameters"></span><span id="input_parameters"></span><span id="INPUT_PARAMETERS"></span>输入参数

[**视频 \_ 请求 \_ 数据包**](/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet) (VRP) **InputBuffer** 包含从显示驱动程序传递的信息。 例如，显示驱动程序可以将指针传递给 \_ 定义为的 COPP IO \_ InputBuffer 结构，如下所示：

```cpp
typedef struct {
    PVOID* ppThis;
    PVOID InputBuffer;
    HRESULT phr;
} COPP_IO_InputBuffer;
```

**PpThis** 成员指向 COPP DirectX VA 设备对象的指针，该对象用于检索硬件证书的大小。 **InputBuffer** 成员不是必需的。 应将 **phr** 成员设置为从 [*COPPGetCertificateLength*](./coppgetcertificatelength.md) 函数返回的值。

### <a name="span-idoutput_parametersspanspan-idoutput_parametersspanspan-idoutput_parametersspanoutput-parameters"></a><span id="Output_Parameters"></span><span id="output_parameters"></span><span id="OUTPUT_PARAMETERS"></span>输出参数

微型端口驱动程序返回指向 VRP **OutputBuffer** 中的 ULONG 类型化变量的指针。 变量包含硬件证书的大小。

### <a name="span-idi_o_status_blockspanspan-idi_o_status_blockspanspan-idi_o_status_blockspanio-status-block"></a><span id="I_O_Status_Block"></span><span id="i_o_status_block"></span><span id="I_O_STATUS_BLOCK"></span>I/o 状态块

微型端口驱动程序将 [**状态 \_ 块**](/windows-hardware/drivers/ddi/video/ns-video-_status_block)结构的 **信息** 成员设置为 sizeof (ULONG) 。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。</p></td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[*COPPGetCertificateLength*](./coppgetcertificatelength.md)

 

