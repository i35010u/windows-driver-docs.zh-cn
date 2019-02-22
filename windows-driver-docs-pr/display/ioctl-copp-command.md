---
title: IOCTL\_COPP\_命令控制代码
description: 执行 COPP DirectX VA 设备上的操作。
ms.assetid: 8593da3d-8e94-4820-91ce-92eb6d624a40
keywords:
- IOCTL_COPP_Command 控制代码的显示设备
topic_type:
- apiref
api_name:
- IOCTL_COPP_Command
api_type:
- NA
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5ebdc39b58672374dcd0a78fce38902b395d2403
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543670"
---
# <a name="ioctlcoppcommand-control-code"></a>IOCTL\_COPP\_命令控制代码


执行 COPP DirectX VA 设备上的操作。

## <span id="ddk_ioctl_copp_command_gg"></span><span id="DDK_IOCTL_COPP_COMMAND_GG"></span>


### <a name="span-idinputparametersspanspan-idinputparametersspanspan-idinputparametersspaninput-parameters"></a><span id="Input_Parameters"></span><span id="input_parameters"></span><span id="INPUT_PARAMETERS"></span>输入的参数

[**视频\_请求\_数据包**](https://msdn.microsoft.com/library/windows/hardware/ff570547) (VRP) **InputBuffer**包含从显示器驱动程序传递的信息。 例如，显示器驱动程序，可以将指针传递到 COPP\_IO\_InputBuffer 结构定义，如下所示：

```cpp
typedef struct {
    PVOID* ppThis;
    PVOID InputBuffer;
    HRESULT phr;
} COPP_IO_InputBuffer;
```

**PpThis**成员指向指向 COPP DirectX VA 设备对象上执行操作。 **InputBuffer**成员设置为指向的指针[ **DXVA\_COPPCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff563141)结构描述 COPP 命令来执行。 **Phr**成员应设置为从返回的值[ *COPPCommand* ](https://msdn.microsoft.com/library/windows/hardware/ff539642)函数。

### <a name="span-idoutputparametersspanspan-idoutputparametersspanspan-idoutputparametersspanoutput-parameters"></a><span id="Output_Parameters"></span><span id="output_parameters"></span><span id="OUTPUT_PARAMETERS"></span>输出参数

无

### <a name="span-idiostatusblockspanspan-idiostatusblockspanspan-idiostatusblockspanio-status-block"></a><span id="I_O_Status_Block"></span><span id="i_o_status_block"></span><span id="I_O_STATUS_BLOCK"></span>I/O 状态块

微型端口驱动程序不会设置**信息**的成员[**状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff569732)结构。

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
<td align="left"><p>本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。</p></td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[*COPPCommand*](https://msdn.microsoft.com/library/windows/hardware/ff539642)

[**DXVA\_COPPCommand**](https://msdn.microsoft.com/library/windows/hardware/ff563141)

 

 






