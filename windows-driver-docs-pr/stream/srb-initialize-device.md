---
title: SRB\_INITIALIZE\_DEVICE
description: SRB\_INITIALIZE\_DEVICE
ms.assetid: a4e35253-43d8-4d11-8a5b-72a9863f6677
keywords:
- SRB_INITIALIZE_DEVICE 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_INITIALIZE_DEVICE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 357f99d56274da7ffcc1b61c5c911f73a29d42ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379948"
---
# <a name="srbinitializedevice"></a>SRB\_INITIALIZE\_DEVICE


## <span id="ddk_srb_initialize_device_ks"></span><span id="DDK_SRB_INITIALIZE_DEVICE_KS"></span>


当它开始初始化微型驱动程序的硬件时，类驱动程序将发送此请求。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应设置以下项之一为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示找到了一个主机适配器的配置信息已成功确定。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态\_IO\_设备\_错误  
指示找到主机适配器，但获取配置信息时出错。 如果可能，应记录错误。

<span id="STATUS_NO_SUCH_DEVICE"></span><span id="status_no_such_device"></span>状态\_否\_SUCH\_设备  
指示提供的配置信息无效。

### <a name="comments"></a>备注

在类驱动程序将指针传递到的端口\_配置\_中的信息结构*pSrb*-&gt;**CommandData.ConfigInfo**。 *PSrb*指针指向[ **HW\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff559702)结构。 找出大多数字段填充的类驱动程序*pSrb*-&gt;**CommandData.ConfigInfo**从操作系统的设备的有关它所获取的信息。 在大多数情况下，微型驱动程序只需填写**StreamDescriptorSize**的成员**ConfigInfo**大小为其[ **HW\_流\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff559686)结构。

 

 





