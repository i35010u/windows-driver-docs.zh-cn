---
title: 支持 OpenGL 增强
description: 支持 OpenGL 增强
ms.assetid: 5f8b7d96-7941-44ce-bd32-546ec0f32883
keywords:
- OpenGL 增强 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23776c9c9de2d5030bb700290786377ada5c05f8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829388"
---
# <a name="supporting-opengl-enhancements"></a>支持 OpenGL 增强


## <a name="span-idwindows_7_enhancementsspanspan-idwindows_7_enhancementsspanspan-idwindows_7_enhancementsspanwindows7-enhancements"></a><span id="Windows_7_Enhancements"></span><span id="windows_7_enhancements"></span><span id="WINDOWS_7_ENHANCEMENTS"></span>Windows 7 增强功能


本部分仅适用于 Windows 7 及更高版本、Windows Server 2008 R2 及更高版本。

可以实现 OpenGL 可安装客户端驱动程序（ICD），使用 Windows 7 随附的以下 OpenGL 增强功能：

### <a name="span-idenhancing_synchronizationspanspan-idenhancing_synchronizationspanenhancing-synchronization"></a><span id="enhancing_synchronization"></span><span id="ENHANCING_SYNCHRONIZATION"></span>增强同步

可以通过使用以下第二代 OpenGL 同步函数增强 OpenGL ICD 的同步功能：

-   [**D3DKMTCreateSynchronizationObject2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtcreatesynchronizationobject2)

-   [**D3DKMTOpenSynchronizationObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopensynchronizationobject)

-   [**D3DKMTWaitForSynchronizationObject2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtwaitforsynchronizationobject2)

-   [**D3DKMTSignalSynchronizationObject2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtsignalsynchronizationobject2)

### <a name="span-idcontrolling_resource_access_with_mutexesspanspan-idcontrolling_resource_access_with_mutexesspancontrolling-resource-access-with-mutexes"></a><span id="controlling_resource_access_with_mutexes"></span><span id="CONTROLLING_RESOURCE_ACCESS_WITH_MUTEXES"></span>使用 Mutex 控制资源访问

你可以使用以下 OpenGL mutex 函数来控制对资源的访问：

-   [**D3DKMTCreateKeyedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtcreatekeyedmutex)

-   [**D3DKMTOpenKeyedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopenkeyedmutex)

-   [**D3DKMTDestroyKeyedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtdestroykeyedmutex)

-   [**D3DKMTAcquireKeyedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtacquirekeyedmutex)

-   [**D3DKMTReleaseKeyedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtreleasekeyedmutex)

### <a name="span-idmanaging_access_to_shared_resourcesspanspan-idmanaging_access_to_shared_resourcesspanmanaging-access-to-shared-resources"></a><span id="managing_access_to_shared_resources"></span><span id="MANAGING_ACCESS_TO_SHARED_RESOURCES"></span>管理对共享资源的访问

你可以使用以下 OpenGL 函数来管理对共享资源的访问：

-   [**D3DKMTConfigureSharedResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtconfiguresharedresource)

-   [**D3DKMTCheckSharedResourceAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtchecksharedresourceaccess)

### <a name="span-idmonitoring_present_historyspanspan-idmonitoring_present_historyspanmonitoring-present-history"></a><span id="monitoring_present_history"></span><span id="MONITORING_PRESENT_HISTORY"></span>监视当前历史记录

你可以使用以下 OpenGL 函数来监视当前操作的历史记录：

-   [**D3DKMTPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtpresent) with [**D3DKMT\_PRESENTHISTORYTOKEN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_presenthistorytoken)结构在[**D3DKMT\_存在**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_present)结构的**PRESENTHISTORYTOKEN**成员中填充

-   [**D3DKMTGetPresentHistory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtgetpresenthistory)

### <a name="span-idmiscellaneous_enhancementsspanspan-idmiscellaneous_enhancementsspanmiscellaneous-enhancements"></a><span id="miscellaneous_enhancements"></span><span id="MISCELLANEOUS_ENHANCEMENTS"></span>其他增强功能

可以使用以下 OpenGL 其他增强功能：

-   [**D3DKMTCheckVidPnExclusiveOwnership**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtcheckvidpnexclusiveownership)

-   [**D3DKMTGetOverlayState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtgetoverlaystate)

-   带有[**D3DKMT\_SETDISPLAYMODE\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_setdisplaymode_flags)结构的[**D3DKMTSetDisplayMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtsetdisplaymode) ，在[**D3DKMT\_SETDISPLAYMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_setdisplaymode)结构的**flags**成员中填充

-   在[**D3DKMT\_POLLDISPLAYCHILDREN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_polldisplaychildren)结构中设置了新标志的[**D3DKMTPollDisplayChildren**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtpolldisplaychildren)

## <a name="span-idwindows_8_enhancementsspanspan-idwindows_8_enhancementsspanwindows8-enhancements"></a><span id="windows_8_enhancements"></span><span id="WINDOWS_8_ENHANCEMENTS"></span>Windows 8 增强功能


本部分仅适用于 Windows 8 及更高版本以及 Windows Server 2012 及更高版本。

可以实现 OpenGL 可安装客户端驱动程序（ICD），使用 Windows 8 随附的以下 OpenGL 增强功能：

### <a name="span-idcontrolling_resource_access_with_mutexes_spanspan-idcontrolling_resource_access_with_mutexes_spanspan-idcontrolling_resource_access_with_mutexes_spancontrolling-resource-access-with-mutexes"></a><span id="Controlling_Resource_Access_with_Mutexes_"></span><span id="controlling_resource_access_with_mutexes_"></span><span id="CONTROLLING_RESOURCE_ACCESS_WITH_MUTEXES_"></span>使用 Mutex 控制资源访问

您可以使用这些 OpenGL mutex 函数和关联结构来控制对资源的访问，同时指定要与键控 mutex 关联的专用数据：

-   [**D3DKMTAcquireKeyedMutex2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtacquirekeyedmutex2)
-   [**D3DKMTCreateKeyedMutex2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtcreatekeyedmutex2)
-   [**D3DKMT\_ACQUIREKEYEDMUTEX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_acquirekeyedmutex2)
-   [**D3DKMT\_CREATEKEYEDMUTEX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_createkeyedmutex2)

### <a name="span-idopengl_helper_functionsspanspan-idopengl_helper_functionsspanspan-idopengl_helper_functionsspanopengl-helper-functions"></a><span id="OpenGL_Helper_Functions"></span><span id="opengl_helper_functions"></span><span id="OPENGL_HELPER_FUNCTIONS"></span>OpenGL Helper 函数

您可以使用这些函数及其关联结构来访问对象及其句柄：

-   [**D3DKMTGetSharedResourceAdapterLuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtgetsharedresourceadapterluid)
-   [**D3DKMTOpenAdapterFromLuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopenadapterfromluid)
-   [**D3DKMTOpenNtHandleFromName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopennthandlefromname)
-   [**D3DKMTOpenResourceFromNtHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopenresourcefromnthandle)
-   [**D3DKMTOpenSyncObjectFromNtHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopensyncobjectfromnthandle)
-   [**D3DKMT\_GETSHAREDRESOURCEADAPTERLUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_getsharedresourceadapterluid)
-   [**D3DKMT\_OPENADAPTERFROMLUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_openadapterfromluid)
-   [**D3DKMT\_OPENNTHANDLEFROMNAME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_opennthandlefromname)
-   [**D3DKMT\_OPENRESOURCEFROMNTHANDLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_openresourcefromnthandle)
-   [**D3DKMT\_OPENSYNCOBJECTFROMNTHANDLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_opensyncobjectfromnthandle)

 

 





