---
title: SRB\_关闭\_设备\_实例
description: SRB\_关闭\_设备\_实例
ms.assetid: 55a72f4f-45b3-427d-80b7-620aac870a8a
keywords:
- SRB_CLOSE_DEVICE_INSTANCE 流媒体设备
topic_type:
- apiref
api_name:
- SRB_CLOSE_DEVICE_INSTANCE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc90976d9f434caebc1e7b049480acf3e6926b60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843311"
---
# <a name="srb_close_device_instance"></a>SRB\_关闭\_设备\_实例


## <span id="ddk_srb_close_device_instance_ks"></span><span id="DDK_SRB_CLOSE_DEVICE_INSTANCE_KS"></span>


类驱动程序发送此请求以关闭以前打开的适配器的实例。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>成功\_状态  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_未\_实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>IO\_设备状态\_\_错误  
指示出现硬件故障。

### <a name="comments"></a>备注

大多数适配器不支持多个实例，因此在这种情况下，FilterInstanceExtensionSize [ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)中的 " " 字段应设置为零，而不会收到此命令。

 

 





