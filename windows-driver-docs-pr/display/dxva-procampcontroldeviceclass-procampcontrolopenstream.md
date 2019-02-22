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
ms.openlocfilehash: 85b4ae38bae3b9b70ec2465d144a48f98cc23efc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555651"
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

<a name="parameters"></a>参数
----------

*lpVideoDescription* \[中\]提供一个指向[ **DXVA\_VideoDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff564070)结构，它定义的 ProcAmp 控件参数要处理的视频。

<a name="return-value"></a>返回值
------------

将返回零 (S\_确定或 DD\_确定) 如果成功; 否则，返回错误代码。 请参阅*ddraw.h*有关错误代码的完整列表。

<a name="remarks"></a>备注
-------

之后*VMR*已确定的功能和范围的使用在 ProcAmp 控件硬件[ **ProcAmpControlQueryCaps** ](dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps.md)和[ **ProcAmpControlQueryRange** ](dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange.md)函数，可以创建 ProcAmp 流对象。 ProcAmp 流对象的创建使显示驱动程序来保留执行 ProcAmp 调整操作所需的硬件资源。

*ProcAmpControlOpenStream*函数将映射到的 CreateMoComp 成员调用的直接[ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)结构。 CreateMoComp 成员指向引用的驱动程序所提供的函数[ **DD\_CREATEMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff550529)结构。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DXVA\_VideoDesc**](https://msdn.microsoft.com/library/windows/hardware/ff564070)

[**DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)

[**DD\_CREATEMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff550529)

[**ProcAmpControlQueryCaps**](dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps.md)

[**ProcAmpControlQueryRange**](dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange.md)

 

 






