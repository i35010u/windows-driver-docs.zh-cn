---
title: 支持 OpenGL 增强
description: 支持 OpenGL 增强
ms.assetid: 5f8b7d96-7941-44ce-bd32-546ec0f32883
keywords:
- OpenGL 增强 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61e6993964eb2e9fb5d537f57c4e78c3c60b5793
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064574"
---
# <a name="supporting-opengl-enhancements"></a>支持 OpenGL 增强


## <a name="span-idwindows_7_enhancementsspanspan-idwindows_7_enhancementsspanspan-idwindows_7_enhancementsspanwindows7-enhancements"></a><span id="Windows_7_Enhancements"></span><span id="windows_7_enhancements"></span><span id="WINDOWS_7_ENHANCEMENTS"></span>Windows 7 增强功能


本部分仅适用于 Windows 7 及更高版本、Windows Server 2008 R2 及更高版本。

可以 (ICD) 实现 OpenGL 可安装客户端驱动程序，使用 Windows 7 随附的以下 OpenGL 增强功能：

### <a name="span-idenhancing_synchronizationspanspan-idenhancing_synchronizationspanenhancing-synchronization"></a><span id="enhancing_synchronization"></span><span id="ENHANCING_SYNCHRONIZATION"></span>增强同步

可以通过使用以下第二代 OpenGL 同步函数增强 OpenGL ICD 的同步功能：

-   [**D3DKMTCreateSynchronizationObject2**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtcreatesynchronizationobject2)

-   [**D3DKMTOpenSynchronizationObject**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopensynchronizationobject)

-   [**D3DKMTWaitForSynchronizationObject2**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtwaitforsynchronizationobject2)

-   [**D3DKMTSignalSynchronizationObject2**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtsignalsynchronizationobject2)

### <a name="span-idcontrolling_resource_access_with_mutexesspanspan-idcontrolling_resource_access_with_mutexesspancontrolling-resource-access-with-mutexes"></a><span id="controlling_resource_access_with_mutexes"></span><span id="CONTROLLING_RESOURCE_ACCESS_WITH_MUTEXES"></span>使用 Mutex 控制资源访问

你可以使用以下 OpenGL mutex 函数来控制对资源的访问：

-   [**D3DKMTCreateKeyedMutex**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtcreatekeyedmutex)

-   [**D3DKMTOpenKeyedMutex**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopenkeyedmutex)

-   [**D3DKMTDestroyKeyedMutex**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtdestroykeyedmutex)

-   [**D3DKMTAcquireKeyedMutex**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtacquirekeyedmutex)

-   [**D3DKMTReleaseKeyedMutex**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtreleasekeyedmutex)

### <a name="span-idmanaging_access_to_shared_resourcesspanspan-idmanaging_access_to_shared_resourcesspanmanaging-access-to-shared-resources"></a><span id="managing_access_to_shared_resources"></span><span id="MANAGING_ACCESS_TO_SHARED_RESOURCES"></span>管理对共享资源的访问

你可以使用以下 OpenGL 函数来管理对共享资源的访问：

-   [**D3DKMTConfigureSharedResource**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtconfiguresharedresource)

-   [**D3DKMTCheckSharedResourceAccess**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtchecksharedresourceaccess)

### <a name="span-idmonitoring_present_historyspanspan-idmonitoring_present_historyspanmonitoring-present-history"></a><span id="monitoring_present_history"></span><span id="MONITORING_PRESENT_HISTORY"></span>监视当前历史记录

你可以使用以下 OpenGL 函数来监视当前操作的历史记录：

-   在[**D3DKMT \_ 存在**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_present)结构的**PRESENTHISTORYTOKEN**成员中填充了[**D3DKMT \_ PRESENTHISTORYTOKEN**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_presenthistorytoken)结构的[**D3DKMTPresent**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtpresent)

-   [**D3DKMTGetPresentHistory**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtgetpresenthistory)

### <a name="span-idmiscellaneous_enhancementsspanspan-idmiscellaneous_enhancementsspanmiscellaneous-enhancements"></a><span id="miscellaneous_enhancements"></span><span id="MISCELLANEOUS_ENHANCEMENTS"></span>其他增强功能

可以使用以下 OpenGL 其他增强功能：

-   [**D3DKMTCheckVidPnExclusiveOwnership**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtcheckvidpnexclusiveownership)

-   [**D3DKMTGetOverlayState**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtgetoverlaystate)

-   [**D3DKMTSetDisplayMode**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtsetdisplaymode)在[**D3DKMT \_ SETDISPLAYMODE**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_setdisplaymode)结构的**FLAGS**成员中填充的[**D3DKMT \_ SETDISPLAYMODE \_ 标志**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_setdisplaymode_flags)结构

-   在[**D3DKMT \_ POLLDISPLAYCHILDREN**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_polldisplaychildren)结构中设置了新标志的[**D3DKMTPollDisplayChildren**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtpolldisplaychildren)

## <a name="span-idwindows_8_enhancementsspanspan-idwindows_8_enhancementsspanwindows8-enhancements"></a><span id="windows_8_enhancements"></span><span id="WINDOWS_8_ENHANCEMENTS"></span>Windows 8 增强功能


本部分仅适用于 Windows 8 及更高版本以及 Windows Server 2012 及更高版本。

可以 (ICD) 实现 OpenGL 可安装客户端驱动程序，以便使用 Windows 8 随附的以下 OpenGL 增强功能：

### <a name="span-idcontrolling_resource_access_with_mutexes_spanspan-idcontrolling_resource_access_with_mutexes_spanspan-idcontrolling_resource_access_with_mutexes_spancontrolling-resource-access-with-mutexes"></a><span id="Controlling_Resource_Access_with_Mutexes_"></span><span id="controlling_resource_access_with_mutexes_"></span><span id="CONTROLLING_RESOURCE_ACCESS_WITH_MUTEXES_"></span>使用 Mutex 控制资源访问

您可以使用这些 OpenGL mutex 函数和关联结构来控制对资源的访问，同时指定要与键控 mutex 关联的专用数据：

-   [**D3DKMTAcquireKeyedMutex2**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtacquirekeyedmutex2)
-   [**D3DKMTCreateKeyedMutex2**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtcreatekeyedmutex2)
-   [**D3DKMT \_ ACQUIREKEYEDMUTEX2**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_acquirekeyedmutex2)
-   [**D3DKMT \_ CREATEKEYEDMUTEX2**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_createkeyedmutex2)

### <a name="span-idopengl_helper_functionsspanspan-idopengl_helper_functionsspanspan-idopengl_helper_functionsspanopengl-helper-functions"></a><span id="OpenGL_Helper_Functions"></span><span id="opengl_helper_functions"></span><span id="OPENGL_HELPER_FUNCTIONS"></span>OpenGL Helper 函数

您可以使用这些函数及其关联结构来访问对象及其句柄：

-   [**D3DKMTGetSharedResourceAdapterLuid**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtgetsharedresourceadapterluid)
-   [**D3DKMTOpenAdapterFromLuid**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopenadapterfromluid)
-   [**D3DKMTOpenNtHandleFromName**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopennthandlefromname)
-   [**D3DKMTOpenResourceFromNtHandle**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopenresourcefromnthandle)
-   [**D3DKMTOpenSyncObjectFromNtHandle**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopensyncobjectfromnthandle)
-   [**D3DKMT \_ GETSHAREDRESOURCEADAPTERLUID**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_getsharedresourceadapterluid)
-   [**D3DKMT \_ OPENADAPTERFROMLUID**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_openadapterfromluid)
-   [**D3DKMT \_ OPENNTHANDLEFROMNAME**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_opennthandlefromname)
-   [**D3DKMT \_ OPENRESOURCEFROMNTHANDLE**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_openresourcefromnthandle)
-   [**D3DKMT \_ OPENSYNCOBJECTFROMNTHANDLE**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_opensyncobjectfromnthandle)

 

