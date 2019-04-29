---
title: SRB\_获取\_设备\_属性
description: SRB\_获取\_设备\_属性
ms.assetid: 2a0a3b8a-7252-4ba5-a1a5-ffef0f0f5715
keywords:
- SRB_GET_DEVICE_PROPERTY 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_GET_DEVICE_PROPERTY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb6c684c785322aa18c7950b4d26f3b8f5e27bd9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390873"
---
# <a name="srbgetdeviceproperty"></a>SRB\_获取\_设备\_属性


## <span id="ddk_srb_get_device_property_ks"></span><span id="DDK_SRB_GET_DEVICE_PROPERTY_KS"></span>


类驱动程序将发送此请求查询微型驱动程序完成微型驱动程序定义的属性上的属性 get 请求所需的数据。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应设置以下项之一为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_不\_实现  
指示该函数不受微型驱动程序。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态\_IO\_设备\_错误  
指示发生了硬件故障。

### <a name="comments"></a>备注

类驱动程序将在操作的参数传递*pSrb*-&gt;**CommandData.PropertyInfo**缓冲，窗体结构[ **流\_属性\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff568442)。 *PSrb*指针指向[ **HW\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff559702)结构。 **属性**流成员\_属性\_说明符所描述的属性有问题，同时**PropertyInfo**成员指定用于复制的属性数据的缓冲区到中。 如果缓冲区太小，微型驱动程序应设置**状态**的成员*pSrb*到状态\_缓冲区\_溢出。

有关属性集的详细信息，请参阅[KS 属性](https://msdn.microsoft.com/library/windows/hardware/ff567671)。

## <a name="see-also"></a>请参阅


[**流\_属性\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff568442)

 

 






