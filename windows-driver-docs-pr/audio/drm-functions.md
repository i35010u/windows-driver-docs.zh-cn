---
title: DRM 函数
description: DRM 函数
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a92d7b56db8e57fa0ea41cfb345f54e208b75ebb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786563"
---
# <a name="drm-functions"></a>DRM 函数


## <span id="ddk_drm_functions_ks"></span><span id="DDK_DRM_FUNCTIONS_KS"></span>


本部分介绍 DRM 函数，这些函数用于管理 Windows 中内核流式传输音频内容的数字版权。 系统驱动程序组件 Drmk.sys 包含这些函数的入口点。 这些函数的定义显示在标头文件 drmk 中。 有关详细信息，请参阅 [数字 Rights Management](./digital-rights-management.md)。

本部分介绍以下 DRM 函数：

[**DrmAddContentHandlers**](/windows-hardware/drivers/ddi/drmk/nf-drmk-drmaddcontenthandlers)

[**DrmCreateContentMixed**](/windows-hardware/drivers/ddi/drmk/nf-drmk-drmcreatecontentmixed)

[**DrmDestroyContent**](/windows-hardware/drivers/ddi/drmk/nf-drmk-drmdestroycontent)

[**DrmForwardContentToDeviceObject**](/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttodeviceobject)

[**DrmForwardContentToFileObject**](/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttofileobject)

[**DrmForwardContentToInterface**](/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttointerface)

[**DrmGetContentRights**](/windows-hardware/drivers/ddi/drmk/nf-drmk-drmgetcontentrights)

此外，本部分还介绍了以下宏：

[**定义 \_ DRMRIGHTS \_ 默认值**](/previous-versions/ff536254(v=vs.85))

 

