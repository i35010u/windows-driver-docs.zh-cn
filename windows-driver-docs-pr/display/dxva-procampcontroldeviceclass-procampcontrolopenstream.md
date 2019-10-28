---
title: ProcAmpControlOpenStream 方法
description: 示例 DXVA\_ProcAmpControlDeviceClass：:P rocAmpControlOpenStream 函数创建 ProcAmp stream 对象。
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
ms.openlocfilehash: 35c43f685416ae21d51ed5535ff1d11bba5a5b60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839712"
---
# <a name="dxva_procampcontroldeviceclassprocampcontrolopenstream-method"></a>DXVA\_ProcAmpControlDeviceClass：:P rocAmpControlOpenStream 方法


示例*ProcAmpControlOpenStream*函数创建 ProcAmp 流对象。

<a name="syntax"></a>语法
------

```cpp
HRESULT ProcAmpControlOpenStream(
  [in] LPDXVA_VideoDesc lpVideoDescription
);
```

<a name="parameters"></a>参数
----------

\] 中的*lpVideoDescription* \[提供一个指向[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)结构的指针，该结构定义要处理的视频的 ProcAmp 控件参数。

<a name="return-value"></a>返回值
------------

如果成功，则返回零（\_确定或 DD\_正常）;否则，将返回错误代码。 有关错误代码的完整列表，请参阅*ddraw。*

<a name="remarks"></a>备注
-------

在*VMR*使用[**ProcAmpControlQueryCaps**](dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps.md)和[**ProcAmpControlQueryRange**](dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange.md)函数确定 ProcAmp 控制硬件的功能和范围之后，就可以创建一个 ProcAmp 流对象了。 创建 ProcAmp stream 对象允许显示驱动程序保留执行 ProcAmp 调整操作所需的硬件资源。

*ProcAmpControlOpenStream*函数直接映射到[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的 CreateMoComp 成员的调用。 CreateMoComp 成员指向驱动程序提供的、引用[**DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)结构的函数。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)

[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)

[**ProcAmpControlQueryCaps**](dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps.md)

[**ProcAmpControlQueryRange**](dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange.md)

 

 






