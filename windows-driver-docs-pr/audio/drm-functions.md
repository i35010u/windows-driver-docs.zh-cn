---
title: DRM 函数
description: DRM 函数
ms.assetid: 7be96ab4-3c27-4e63-b0dd-71d814d804d7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23df55369de4062f0d62bb58e2473524555dc512
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833438"
---
# <a name="drm-functions"></a>DRM 函数


## <span id="ddk_drm_functions_ks"></span><span id="DDK_DRM_FUNCTIONS_KS"></span>


本部分介绍 DRM 函数，这些函数用于管理 Windows 中内核流式传输音频内容的数字版权。 系统驱动程序组件 Drmk 包含这些函数的入口点。 这些函数的定义显示在标头文件 drmk 中。 有关详细信息，请参阅[数字 Rights Management](https://docs.microsoft.com/windows-hardware/drivers/audio/digital-rights-management)。

本部分介绍以下 DRM 函数：

[**DrmAddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmaddcontenthandlers)

[**DrmCreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmcreatecontentmixed)

[**DrmDestroyContent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmdestroycontent)

[**DrmForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttodeviceobject)

[**DrmForwardContentToFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttofileobject)

[**DrmForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttointerface)

[**DrmGetContentRights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmgetcontentrights)

此外，本部分还介绍了以下宏：

[**定义\_DRMRIGHTS\_默认值**](https://docs.microsoft.com/previous-versions/ff536254(v=vs.85))

 

 





