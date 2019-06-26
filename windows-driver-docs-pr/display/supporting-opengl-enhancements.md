---
title: 支持 OpenGL 增强
description: 支持 OpenGL 增强
ms.assetid: 5f8b7d96-7941-44ce-bd32-546ec0f32883
keywords:
- OpenGL 的增强功能 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b42632146be865b3ca2f0244dddf6c6690ce4cd7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380534"
---
# <a name="supporting-opengl-enhancements"></a>支持 OpenGL 增强


## <a name="span-idwindows7enhancementsspanspan-idwindows7enhancementsspanspan-idwindows7enhancementsspanwindows7-enhancements"></a><span id="Windows_7_Enhancements"></span><span id="windows_7_enhancements"></span><span id="WINDOWS_7_ENHANCEMENTS"></span>Windows 7 增强功能


本部分仅适用于 Windows 7 和更高版本，Windows Server 2008 R2 和更高版本。

您可以实现您的 OpenGL 可安装的客户端驱动程序 (ICD) 以用于 Windows 7 附带以下 OpenGL 增强功能：

### <a name="span-idenhancingsynchronizationspanspan-idenhancingsynchronizationspanenhancing-synchronization"></a><span id="enhancing_synchronization"></span><span id="ENHANCING_SYNCHRONIZATION"></span>增强的同步

使用以下的第二代 OpenGL 同步函数，可以提高性能 OpenGL ICD 同步的功能：

-   [**D3DKMTCreateSynchronizationObject2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtcreatesynchronizationobject2)

-   [**D3DKMTOpenSynchronizationObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtopensynchronizationobject)

-   [**D3DKMTWaitForSynchronizationObject2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtwaitforsynchronizationobject2)

-   [**D3DKMTSignalSynchronizationObject2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtsignalsynchronizationobject2)

### <a name="span-idcontrollingresourceaccesswithmutexesspanspan-idcontrollingresourceaccesswithmutexesspancontrolling-resource-access-with-mutexes"></a><span id="controlling_resource_access_with_mutexes"></span><span id="CONTROLLING_RESOURCE_ACCESS_WITH_MUTEXES"></span>控制资源访问的互斥锁

以下 OpenGL 互斥体函数可用于控制对资源的访问：

-   [**D3DKMTCreateKeyedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtcreatekeyedmutex)

-   [**D3DKMTOpenKeyedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtopenkeyedmutex)

-   [**D3DKMTDestroyKeyedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtdestroykeyedmutex)

-   [**D3DKMTAcquireKeyedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtacquirekeyedmutex)

-   [**D3DKMTReleaseKeyedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtreleasekeyedmutex)

### <a name="span-idmanagingaccesstosharedresourcesspanspan-idmanagingaccesstosharedresourcesspanmanaging-access-to-shared-resources"></a><span id="managing_access_to_shared_resources"></span><span id="MANAGING_ACCESS_TO_SHARED_RESOURCES"></span>管理对共享资源的访问

以下的 OpenGL 函数可用于管理对共享资源的访问：

-   [**D3DKMTConfigureSharedResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtconfiguresharedresource)

-   [**D3DKMTCheckSharedResourceAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtchecksharedresourceaccess)

### <a name="span-idmonitoringpresenthistoryspanspan-idmonitoringpresenthistoryspanmonitoring-present-history"></a><span id="monitoring_present_history"></span><span id="MONITORING_PRESENT_HISTORY"></span>监视存在历史记录

以下的 OpenGL 函数可用于监视存在操作的历史记录：

-   [**D3DKMTPresent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtpresent)与[ **D3DKMT\_PRESENTHISTORYTOKEN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_presenthistorytoken)结构中填充**PresentHistoryToken**成员[ **D3DKMT\_存在**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_present)结构

-   [**D3DKMTGetPresentHistory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtgetpresenthistory)

### <a name="span-idmiscellaneousenhancementsspanspan-idmiscellaneousenhancementsspanmiscellaneous-enhancements"></a><span id="miscellaneous_enhancements"></span><span id="MISCELLANEOUS_ENHANCEMENTS"></span>其他增强功能

可以使用以下 OpenGL 其他增强功能：

-   [**D3DKMTCheckVidPnExclusiveOwnership**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtcheckvidpnexclusiveownership)

-   [**D3DKMTGetOverlayState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtgetoverlaystate)

-   [**D3DKMTSetDisplayMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtsetdisplaymode)与[ **D3DKMT\_SETDISPLAYMODE\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_setdisplaymode_flags)结构中填充**标志**的成员[ **D3DKMT\_SETDISPLAYMODE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_setdisplaymode)结构

-   [**D3DKMTPollDisplayChildren** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtpolldisplaychildren)中设置的新标志与[ **D3DKMT\_POLLDISPLAYCHILDREN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_polldisplaychildren)结构

## <a name="span-idwindows8enhancementsspanspan-idwindows8enhancementsspanwindows8-enhancements"></a><span id="windows_8_enhancements"></span><span id="WINDOWS_8_ENHANCEMENTS"></span>Windows 8 的增强功能


本部分仅适用于 Windows 8 及更高版本、 和 Windows Server 2012 及更高版本。

您可以实现您的 OpenGL 可安装的客户端驱动程序 (ICD) 以用于 Windows 8 提供的以下 OpenGL 增强功能：

### <a name="span-idcontrollingresourceaccesswithmutexesspanspan-idcontrollingresourceaccesswithmutexesspanspan-idcontrollingresourceaccesswithmutexesspancontrolling-resource-access-with-mutexes"></a><span id="Controlling_Resource_Access_with_Mutexes_"></span><span id="controlling_resource_access_with_mutexes_"></span><span id="CONTROLLING_RESOURCE_ACCESS_WITH_MUTEXES_"></span>控制资源访问的互斥锁

可以使用这些 OpenGL 互斥体函数和关联结构，以指定要将与键控的互斥体相关联的私有数据时控制对资源的访问：

-   [**D3DKMTAcquireKeyedMutex2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtacquirekeyedmutex2)
-   [**D3DKMTCreateKeyedMutex2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtcreatekeyedmutex2)
-   [**D3DKMT\_ACQUIREKEYEDMUTEX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_acquirekeyedmutex2)
-   [**D3DKMT\_CREATEKEYEDMUTEX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_createkeyedmutex2)

### <a name="span-idopenglhelperfunctionsspanspan-idopenglhelperfunctionsspanspan-idopenglhelperfunctionsspanopengl-helper-functions"></a><span id="OpenGL_Helper_Functions"></span><span id="opengl_helper_functions"></span><span id="OPENGL_HELPER_FUNCTIONS"></span>OpenGL 帮助器函数

可以使用这些函数和其关联的结构来访问对象和其句柄：

-   [**D3DKMTGetSharedResourceAdapterLuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtgetsharedresourceadapterluid)
-   [**D3DKMTOpenAdapterFromLuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtopenadapterfromluid)
-   [**D3DKMTOpenNtHandleFromName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtopennthandlefromname)
-   [**D3DKMTOpenResourceFromNtHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtopenresourcefromnthandle)
-   [**D3DKMTOpenSyncObjectFromNtHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtopensyncobjectfromnthandle)
-   [**D3DKMT\_GETSHAREDRESOURCEADAPTERLUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_getsharedresourceadapterluid)
-   [**D3DKMT\_OPENADAPTERFROMLUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_openadapterfromluid)
-   [**D3DKMT\_OPENNTHANDLEFROMNAME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_opennthandlefromname)
-   [**D3DKMT\_OPENRESOURCEFROMNTHANDLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_openresourcefromnthandle)
-   [**D3DKMT\_OPENSYNCOBJECTFROMNTHANDLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_opensyncobjectfromnthandle)

 

 





