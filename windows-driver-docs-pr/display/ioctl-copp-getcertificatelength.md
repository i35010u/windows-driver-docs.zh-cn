---
title: IOCTL\_COPP\_GetCertificateLength 控制代码
description: 返回的大小，以字节为单位的图形硬件使用的证书。
ms.assetid: a65d301a-4b33-45f9-b21e-a2606d752b12
keywords:
- IOCTL_COPP_GetCertificateLength 控制代码的显示设备
topic_type:
- apiref
api_name:
- IOCTL_COPP_GetCertificateLength
api_type:
- NA
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f076ba80f3daf0432ceee92d860ce1aa5b1913f4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372921"
---
# <a name="ioctlcoppgetcertificatelength-control-code"></a>IOCTL\_COPP\_GetCertificateLength 控制代码


返回的大小，以字节为单位的图形硬件使用的证书。

## <span id="ddk_ioctl_copp_getcertificatelength_gg"></span><span id="DDK_IOCTL_COPP_GETCERTIFICATELENGTH_GG"></span>


### <a name="span-idinputparametersspanspan-idinputparametersspanspan-idinputparametersspaninput-parameters"></a><span id="Input_Parameters"></span><span id="input_parameters"></span><span id="INPUT_PARAMETERS"></span>输入的参数

[**视频\_请求\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_request_packet) (VRP) **InputBuffer**包含从显示器驱动程序传递的信息。 例如，显示器驱动程序，可以将指针传递到 COPP\_IO\_InputBuffer 结构定义，如下所示：

```cpp
typedef struct {
    PVOID* ppThis;
    PVOID InputBuffer;
    HRESULT phr;
} COPP_IO_InputBuffer;
```

**PpThis**成员指向指向 COPP DirectX VA 设备对象，该对象用于检索硬件证书的大小。 **InputBuffer**成员不需要。 **Phr**成员应设置为从返回的值[ *COPPGetCertificateLength* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppgetcertificatelength)函数。

### <a name="span-idoutputparametersspanspan-idoutputparametersspanspan-idoutputparametersspanoutput-parameters"></a><span id="Output_Parameters"></span><span id="output_parameters"></span><span id="OUTPUT_PARAMETERS"></span>输出参数

微型端口驱动程序返回一个指向 ULONG 类型化变量中 VRP **OutputBuffer**。 变量可保留硬件证书的大小。

### <a name="span-idiostatusblockspanspan-idiostatusblockspanspan-idiostatusblockspanio-status-block"></a><span id="I_O_Status_Block"></span><span id="i_o_status_block"></span><span id="I_O_STATUS_BLOCK"></span>I/O 状态块

微型端口驱动程序集**信息**的成员[**状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_status_block) sizeof(ULONG) 的结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。</p></td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[*COPPGetCertificateLength*](https://docs.microsoft.com/windows-hardware/drivers/display/coppgetcertificatelength)

 

 






