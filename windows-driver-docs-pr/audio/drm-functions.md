---
title: DRM 函数
description: DRM 函数
ms.assetid: 7be96ab4-3c27-4e63-b0dd-71d814d804d7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a521d86630171325d3e2fa2cbc4719c563a592a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360098"
---
# <a name="drm-functions"></a>DRM 函数


## <span id="ddk_drm_functions_ks"></span><span id="DDK_DRM_FUNCTIONS_KS"></span>


本部分介绍驱动程序用于管理 Windows 的内核流式处理音频内容的数字权限的 DRM 函数。 系统驱动程序组件 Drmk.sys 包含这些函数的入口点。 这些函数的定义出现在标头文件 drmk.h。 有关详细信息，请参阅[数字权限管理](https://docs.microsoft.com/windows-hardware/drivers/audio/digital-rights-management)。

本部分介绍了以下 DRM 函数：

[**DrmAddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmaddcontenthandlers)

[**DrmCreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmcreatecontentmixed)

[**DrmDestroyContent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmdestroycontent)

[**DrmForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmforwardcontenttodeviceobject)

[**DrmForwardContentToFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmforwardcontenttofileobject)

[**DrmForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmforwardcontenttointerface)

[**DrmGetContentRights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmgetcontentrights)

此外，本部分介绍以下宏：

[**定义\_DRMRIGHTS\_默认**](https://docs.microsoft.com/previous-versions/ff536254(v=vs.85))

 

 





