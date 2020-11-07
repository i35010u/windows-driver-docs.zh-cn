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
ms.openlocfilehash: 4c25fb66d89e8983afbd44e8ebdffcf1f2dfee74
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361286"
---
# <a name="dxva_deinterlacebobdeviceclassdeinterlaceopenstream-method"></a>DXVA \_ DeinterlaceBobDeviceClass：:D einterlaceopenstream 方法


示例 *DeinterlaceOpenStream* 函数创建并打开一个隔行扫描流对象。

<a name="syntax"></a>语法
------

```cpp
HRESULT DeinterlaceOpenStream(
  [in] LPDXVA_VideoDesc lpVideoDescription
);
```

<a name="parameters"></a>参数
----------

*lpVideoDescription* \[在中， \] 提供指向 [**DXVA \_ VideoDesc**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc) 结构的指针，该结构指示要 deinterlaced 或转换速率的视频类型。 将指针传递给驱动程序，以便驱动程序可以支持源视频的分辨率和格式。 例如，驱动程序可能能够对480i 的内容执行三字段自适应隔行扫描，但它可能只允许 bob 1080i 内容。 所有驱动程序都应该能够使用现有的 *位块传输* 硬件支持 bob。

<a name="return-value"></a>返回值
------------

如果成功，则返回零 (S \_ 正常或 DD \_ 确定) ; 否则返回错误代码。 有关错误代码的完整列表，请参阅 *ddraw。*

<a name="remarks"></a>备注
-------

使用 [**DeinterlaceQueryAvailableModes**](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md) 函数找到隔行扫描模式 GUID 后，就可以创建取消隔行扫描流对象了。 此对象允许显示驱动程序保留执行请求的隔行扫描操作所需的任何硬件资源。

有关驱动程序如何使用 *lpVideoDescription* 参数提供的信息执行取消隔行转换或帧速率转换操作的详细信息，请参阅 [用于取消隔行扫描和 Frame-Rate 转换的视频内容](./video-content-for-deinterlace-and-frame-rate-conversion.md)。

示例 *DeinterlaceOpenStream* 函数直接映射到 [**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的 **CreateMoComp** 成员，其中 GUID 是请求的取消隔行扫描模式。 [**DD \_ CREATEMOCOMPDATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_createmocompdata)结构的 **lpData** 成员指向 [**DXVA \_ VideoDesc**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)结构。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD \_ CREATEMOCOMPDATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_createmocompdata)

[**DeinterlaceQueryAvailableModes**](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)

[**DXVA \_ VideoDesc**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)

