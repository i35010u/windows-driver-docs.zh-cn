---
title: DeinterlaceCloseStream 方法
description: 示例 DXVA \_ DeinterlaceBobDeviceClass：:D einterlaceclosestream 函数关闭取消隔行扫描流对象，并指示设备驱动程序释放与该流关联的任何硬件资源。
keywords:
- DeinterlaceCloseStream 方法显示设备
- DeinterlaceCloseStream 方法显示设备，DXVA_DeinterlaceBobDeviceClass 接口
- DXVA_DeinterlaceBobDeviceClass 接口显示设备，DeinterlaceCloseStream 方法
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceBobDeviceClass.DeinterlaceCloseStream
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: c8cf83301ff2746286fd24f20cae4a560cedc4a9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808891"
---
# <a name="dxva_deinterlacebobdeviceclassdeinterlaceclosestream-method"></a>DXVA \_ DeinterlaceBobDeviceClass：:D einterlaceclosestream 方法


示例 *DeinterlaceCloseStream* 函数关闭取消隔行扫描流对象，并指示设备驱动程序释放与该流关联的任何硬件资源。

<a name="syntax"></a>语法
------

```cpp
HRESULT DeinterlaceCloseStream();
```

<a name="parameters"></a>参数
----------

此方法没有任何参数。

<a name="return-value"></a>返回值
------------

如果成功，则返回零 (S \_ 正常或 DD \_ 确定) ; 否则返回错误代码。 有关错误代码的完整列表，请参阅 *ddraw。*

<a name="remarks"></a>备注
-------

*DeinterlaceCloseStream* 函数直接映射到 [**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的 **DestroyMoComp** 成员，该成员指向驱动程序提供的 *DdMoCompDestroy* 回调。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DeinterlaceOpenStream**](dxva-deinterlacebobdeviceclass-deinterlaceopenstream.md)

 

