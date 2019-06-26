---
title: ProcAmpControlCloseStream 方法
description: 示例 DXVA\_ProcAmpControlDeviceClass::ProcAmpCloseStream 函数关闭 ProcAmp 流对象，并指示释放与该流关联的硬件资源的设备驱动程序。
ms.assetid: aa13efb8-2014-4790-b121-cd9fd3171458
keywords:
- ProcAmpControlCloseStream 方法显示设备
- ProcAmpControlCloseStream 方法显示设备，DXVA_ProcAmpControlDeviceClass 接口
- DXVA_ProcAmpControlDeviceClass 接口显示设备，ProcAmpControlCloseStream 方法
topic_type:
- apiref
api_name:
- DXVA_ProcAmpControlDeviceClass.ProcAmpControlCloseStream
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 1aa6b4d6ff0207581b2a11bc1e43c1c75c4c28b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383100"
---
# <a name="dxvaprocampcontroldeviceclassprocampcontrolclosestream-method"></a>DXVA\_ProcAmpControlDeviceClass::ProcAmpControlCloseStream 方法


该示例**ProcAmpCloseStream**函数关闭 ProcAmp 流对象，并指示释放与该流关联的硬件资源的设备驱动程序。

<a name="syntax"></a>语法
------

```cpp
HRESULT ProcAmpControlCloseStream(
   void
);
```

<a name="parameters"></a>Parameters
----------

\* * 无

<a name="return-value"></a>返回值
------------

将返回零 (S\_确定或 DD\_确定) 如果成功; 否则，返回错误代码。 请参阅*ddraw.h*有关错误代码的完整列表。

<a name="remarks"></a>备注
-------

**ProcAmpControlCloseStream**函数直接映射到**DestroyMoComp**的成员[ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构，它指向的驱动程序提供[ *DdMoCompDestroy* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)回调。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**ProcAmpControlOpenStream**](dxva-procampcontroldeviceclass-procampcontrolopenstream.md)

 

 






