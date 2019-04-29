---
title: DeinterlaceOpenStream 方法
description: 示例 DXVA_DeinterlaceBobDeviceClass::DeinterlaceOpenStream 函数创建并打开取消隔行扫描流对象。
ms.assetid: 975d5f6a-8d92-4da5-846c-1637fca58eb1
keywords:
- DeinterlaceOpenStream 方法显示设备
- DeinterlaceOpenStream 方法显示设备，DXVA_DeinterlaceBobDeviceClass 接口
- DXVA_DeinterlaceBobDeviceClass 接口显示设备，DeinterlaceOpenStream 方法
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceBobDeviceClass.DeinterlaceOpenStream
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 614d6dfa6fdee4d9496af412031ef003828d8a20
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357685"
---
# <a name="dxvadeinterlacebobdeviceclassdeinterlaceopenstream-method"></a>DXVA\_DeinterlaceBobDeviceClass::DeinterlaceOpenStream 方法


该示例*DeinterlaceOpenStream*函数创建并打开取消隔行扫描流对象。

<a name="syntax"></a>语法
------

```cpp
HRESULT DeinterlaceOpenStream(
  [in] LPDXVA_VideoDesc lpVideoDescription
);
```

<a name="parameters"></a>Parameters
----------

*lpVideoDescription* \[中\]提供一个指向**DXVA\_VideoDesc**硬件。

<a name="return-value"></a>返回值
------------

将返回零 (S\_确定或 DD\_确定) 如果成功; 否则，返回错误代码。 请参阅*ddraw.h*有关错误代码的完整列表。

<a name="remarks"></a>备注
-------

在取消隔行扫描模式后，GUID 找到使用[ **DeinterlaceQueryAvailableModes** ](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)函数，可以创建取消隔行扫描流对象。 此对象允许显示驱动程序保留的任何硬件资源所需执行请求的取消隔行扫描操作。

详细了解驱动程序的执行方式取消隔行扫描或使用信息的帧速率转换操作提供的*lpVideoDescription*参数，请参阅[的取消隔行扫描内容的视频和帧速率转换](https://msdn.microsoft.com/library/windows/hardware/ff570502)。

该示例*DeinterlaceOpenStream*函数直接映射到**CreateMoComp**的成员[ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)结构，其中 GUID 是请求的取消隔行扫描模式。 **LpData**的成员[ **DD\_CREATEMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff550529)结构指向[ **DXVA\_VideoDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff564070)结构。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)

[**DD\_CREATEMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff550529)

[**DeinterlaceQueryAvailableModes**](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)

[**DXVA\_VideoDesc**](https://msdn.microsoft.com/library/windows/hardware/ff564070)

 

 






