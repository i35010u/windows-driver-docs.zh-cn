---
title: DeinterlaceOpenStream 方法
description: 示例 DXVA_DeinterlaceBobDeviceClass：:D einterlaceOpenStream 函数创建并打开一个隔行扫描流对象。
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
ms.openlocfilehash: d5b2a01fc74d0c2bc76638d01d40b70ef2ed3709
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838968"
---
# <a name="dxva_deinterlacebobdeviceclassdeinterlaceopenstream-method"></a>DXVA\_DeinterlaceBobDeviceClass：:D einterlaceOpenStream 方法


示例*DeinterlaceOpenStream*函数创建并打开一个隔行扫描流对象。

<a name="syntax"></a>语法
------

```cpp
HRESULT DeinterlaceOpenStream(
  [in] LPDXVA_VideoDesc lpVideoDescription
);
```

<a name="parameters"></a>参数
----------

\] 中的*lpVideoDescription* \[提供指向**DXVA\_VideoDesc**硬件的指针。

<a name="return-value"></a>返回值
------------

如果成功，则返回零（\_确定或 DD\_正常）;否则，将返回错误代码。 有关错误代码的完整列表，请参阅*ddraw。*

<a name="remarks"></a>备注
-------

使用[**DeinterlaceQueryAvailableModes**](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)函数找到隔行扫描模式 GUID 后，就可以创建取消隔行扫描流对象了。 此对象允许显示驱动程序保留执行请求的隔行扫描操作所需的任何硬件资源。

有关驱动程序如何使用*lpVideoDescription*参数提供的信息执行取消隔行转换或帧速率转换操作的详细信息，请参阅[视频内容进行取消隔行扫描和帧速率转换](https://docs.microsoft.com/windows-hardware/drivers/display/video-content-for-deinterlace-and-frame-rate-conversion)。

示例*DeinterlaceOpenStream*函数直接映射到[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的**CreateMoComp**成员，其中 GUID 是请求的取消隔行扫描模式。 [**DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)结构的**LpData**成员指向[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)结构。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)

[**DeinterlaceQueryAvailableModes**](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)

[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)

 

 






