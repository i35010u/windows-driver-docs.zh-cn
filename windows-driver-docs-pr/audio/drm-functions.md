---
title: DRM 函数
description: DRM 函数
ms.assetid: 7be96ab4-3c27-4e63-b0dd-71d814d804d7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 619ae36d96ca1f7e7ba16255731a754aaa72b6f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564940"
---
# <a name="drm-functions"></a>DRM 函数


## <span id="ddk_drm_functions_ks"></span><span id="DDK_DRM_FUNCTIONS_KS"></span>


本部分介绍驱动程序用于管理 Windows 的内核流式处理音频内容的数字权限的 DRM 函数。 系统驱动程序组件 Drmk.sys 包含这些函数的入口点。 这些函数的定义出现在标头文件 drmk.h。 有关详细信息，请参阅[数字权限管理](https://msdn.microsoft.com/library/windows/hardware/ff536260)。

本部分介绍了以下 DRM 函数：

[**DrmAddContentHandlers**](https://msdn.microsoft.com/library/windows/hardware/ff536347)

[**DrmCreateContentMixed**](https://msdn.microsoft.com/library/windows/hardware/ff536348)

[**DrmDestroyContent**](https://msdn.microsoft.com/library/windows/hardware/ff536349)

[**DrmForwardContentToDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff536351)

[**DrmForwardContentToFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff536352)

[**DrmForwardContentToInterface**](https://msdn.microsoft.com/library/windows/hardware/ff536353)

[**DrmGetContentRights**](https://msdn.microsoft.com/library/windows/hardware/ff536354)

此外，本部分介绍以下宏：

[**定义\_DRMRIGHTS\_默认**](https://msdn.microsoft.com/library/windows/hardware/ff536254)

 

 





