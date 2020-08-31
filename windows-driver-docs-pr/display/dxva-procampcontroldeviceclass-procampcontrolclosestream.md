---
title: ProcAmpControlCloseStream 方法
description: 示例 DXVA \_ ProcAmpControlDeviceClass：:P rocampclosestream 函数关闭 ProcAmp stream 对象，并指示设备驱动程序释放与该流关联的硬件资源。
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
ms.openlocfilehash: 324a7638fd2b49dc5dfdb211c05fa5198447fb36
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063104"
---
# <a name="dxva_procampcontroldeviceclassprocampcontrolclosestream-method"></a>DXVA \_ ProcAmpControlDeviceClass：:P rocampcontrolclosestream 方法


示例 **ProcAmpCloseStream** 函数关闭 ProcAmp 流对象，并指示设备驱动程序释放与该流关联的硬件资源。

<a name="syntax"></a>语法
------

```cpp
HRESULT ProcAmpControlCloseStream(
   void
);
```

<a name="parameters"></a>parameters
----------

* * 无

<a name="return-value"></a>返回值
------------

如果成功，则返回零 (S \_ 正常或 DD \_ 确定) ; 否则返回错误代码。 有关错误代码的完整列表，请参阅*ddraw。*

<a name="remarks"></a>备注
-------

**ProcAmpControlCloseStream**函数直接映射到[**DD \_ MOTIONCOMPCALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的**DestroyMoComp**成员，该成员指向驱动程序提供的[*DdMoCompDestroy*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)回调。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**DD \_ MOTIONCOMPCALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**ProcAmpControlOpenStream**](dxva-procampcontroldeviceclass-procampcontrolopenstream.md)

 

