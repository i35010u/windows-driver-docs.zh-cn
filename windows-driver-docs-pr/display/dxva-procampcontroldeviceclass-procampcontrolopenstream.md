---
title: ProcAmpControlOpenStream 方法
description: 示例 DXVA\_ProcAmpControlDeviceClass::ProcAmpControlOpenStream 函数创建 ProcAmp 流对象。
ms.assetid: 73011ce3-f643-4fca-bcfd-1467a9b56181
keywords:
- ProcAmpControlOpenStream 方法显示设备
- ProcAmpControlOpenStream 方法显示设备，DXVA_ProcAmpControlDeviceClass 接口
- DXVA_ProcAmpControlDeviceClass 接口显示设备，ProcAmpControlOpenStream 方法
topic_type:
- apiref
api_name:
- DXVA_ProcAmpControlDeviceClass.ProcAmpControlOpenStream
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: ceefb1472fc09c3c6f403c8e308e9c1deacaffa8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375815"
---
# <a name="dxvaprocampcontroldeviceclassprocampcontrolopenstream-method"></a>DXVA\_ProcAmpControlDeviceClass::ProcAmpControlOpenStream 方法


该示例*ProcAmpControlOpenStream*函数创建 ProcAmp 流对象。

<a name="syntax"></a>语法
------

```cpp
HRESULT ProcAmpControlOpenStream(
  [in] LPDXVA_VideoDesc lpVideoDescription
);
```

<a name="parameters"></a>Parameters
----------

*lpVideoDescription* \[中\]提供一个指向[ **DXVA\_VideoDesc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)结构，它定义的 ProcAmp 控件参数要处理的视频。

<a name="return-value"></a>返回值
------------

将返回零 (S\_确定或 DD\_确定) 如果成功; 否则，返回错误代码。 请参阅*ddraw.h*有关错误代码的完整列表。

<a name="remarks"></a>备注
-------

之后*VMR*已确定的功能和范围的使用在 ProcAmp 控件硬件[ **ProcAmpControlQueryCaps** ](dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps.md)和[ **ProcAmpControlQueryRange** ](dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange.md)函数，可以创建 ProcAmp 流对象。 ProcAmp 流对象的创建使显示驱动程序来保留执行 ProcAmp 调整操作所需的硬件资源。

*ProcAmpControlOpenStream*函数将映射到的 CreateMoComp 成员调用的直接[ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构。 CreateMoComp 成员指向引用的驱动程序所提供的函数[ **DD\_CREATEMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)结构。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)

[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)

[**ProcAmpControlQueryCaps**](dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps.md)

[**ProcAmpControlQueryRange**](dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange.md)

 

 






