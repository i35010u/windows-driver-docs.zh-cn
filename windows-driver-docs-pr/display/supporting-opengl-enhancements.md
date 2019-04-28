---
title: 支持 OpenGL 增强
description: 支持 OpenGL 增强
ms.assetid: 5f8b7d96-7941-44ce-bd32-546ec0f32883
keywords:
- OpenGL 的增强功能 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f81cd62fba565a03252a41c7e9153981a7aabdf7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350222"
---
# <a name="supporting-opengl-enhancements"></a>支持 OpenGL 增强


## <a name="span-idwindows7enhancementsspanspan-idwindows7enhancementsspanspan-idwindows7enhancementsspanwindows7-enhancements"></a><span id="Windows_7_Enhancements"></span><span id="windows_7_enhancements"></span><span id="WINDOWS_7_ENHANCEMENTS"></span>Windows 7 增强功能


本部分仅适用于 Windows 7 和更高版本，Windows Server 2008 R2 和更高版本。

您可以实现您的 OpenGL 可安装的客户端驱动程序 (ICD) 以用于 Windows 7 附带以下 OpenGL 增强功能：

### <a name="span-idenhancingsynchronizationspanspan-idenhancingsynchronizationspanenhancing-synchronization"></a><span id="enhancing_synchronization"></span><span id="ENHANCING_SYNCHRONIZATION"></span>增强的同步

使用以下的第二代 OpenGL 同步函数，可以提高性能 OpenGL ICD 同步的功能：

-   [**D3DKMTCreateSynchronizationObject2**](https://msdn.microsoft.com/library/windows/hardware/ff546879)

-   [**D3DKMTOpenSynchronizationObject**](https://msdn.microsoft.com/library/windows/hardware/ff547069)

-   [**D3DKMTWaitForSynchronizationObject2**](https://msdn.microsoft.com/library/windows/hardware/ff547262)

-   [**D3DKMTSignalSynchronizationObject2**](https://msdn.microsoft.com/library/windows/hardware/ff547227)

### <a name="span-idcontrollingresourceaccesswithmutexesspanspan-idcontrollingresourceaccesswithmutexesspancontrolling-resource-access-with-mutexes"></a><span id="controlling_resource_access_with_mutexes"></span><span id="CONTROLLING_RESOURCE_ACCESS_WITH_MUTEXES"></span>控制资源访问的互斥锁

以下 OpenGL 互斥体函数可用于控制对资源的访问：

-   [**D3DKMTCreateKeyedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff546845)

-   [**D3DKMTOpenKeyedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff547054)

-   [**D3DKMTDestroyKeyedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff546920)

-   [**D3DKMTAcquireKeyedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff546732)

-   [**D3DKMTReleaseKeyedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff547129)

### <a name="span-idmanagingaccesstosharedresourcesspanspan-idmanagingaccesstosharedresourcesspanmanaging-access-to-shared-resources"></a><span id="managing_access_to_shared_resources"></span><span id="MANAGING_ACCESS_TO_SHARED_RESOURCES"></span>管理对共享资源的访问

以下的 OpenGL 函数可用于管理对共享资源的访问：

-   [**D3DKMTConfigureSharedResource**](https://msdn.microsoft.com/library/windows/hardware/ff546798)

-   [**D3DKMTCheckSharedResourceAccess**](https://msdn.microsoft.com/library/windows/hardware/ff546769)

### <a name="span-idmonitoringpresenthistoryspanspan-idmonitoringpresenthistoryspanmonitoring-present-history"></a><span id="monitoring_present_history"></span><span id="MONITORING_PRESENT_HISTORY"></span>监视存在历史记录

以下的 OpenGL 函数可用于监视存在操作的历史记录：

-   [**D3DKMTPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff547091)与[ **D3DKMT\_PRESENTHISTORYTOKEN** ](https://msdn.microsoft.com/library/windows/hardware/ff548188)结构中填充**PresentHistoryToken**成员[ **D3DKMT\_存在**](https://msdn.microsoft.com/library/windows/hardware/ff548168)结构

-   [**D3DKMTGetPresentHistory**](https://msdn.microsoft.com/library/windows/hardware/ff546987)

### <a name="span-idmiscellaneousenhancementsspanspan-idmiscellaneousenhancementsspanmiscellaneous-enhancements"></a><span id="miscellaneous_enhancements"></span><span id="MISCELLANEOUS_ENHANCEMENTS"></span>其他增强功能

可以使用以下 OpenGL 其他增强功能：

-   [**D3DKMTCheckVidPnExclusiveOwnership**](https://msdn.microsoft.com/library/windows/hardware/ff546779)

-   [**D3DKMTGetOverlayState**](https://msdn.microsoft.com/library/windows/hardware/ff546977)

-   [**D3DKMTSetDisplayMode** ](https://msdn.microsoft.com/library/windows/hardware/ff547169)与[ **D3DKMT\_SETDISPLAYMODE\_标志**](https://msdn.microsoft.com/library/windows/hardware/ff548286)结构中填充**标志**的成员[ **D3DKMT\_SETDISPLAYMODE** ](https://msdn.microsoft.com/library/windows/hardware/ff548275)结构

-   [**D3DKMTPollDisplayChildren** ](https://msdn.microsoft.com/library/windows/hardware/ff547077)中设置的新标志与[ **D3DKMT\_POLLDISPLAYCHILDREN** ](https://msdn.microsoft.com/library/windows/hardware/ff548161)结构

## <a name="span-idwindows8enhancementsspanspan-idwindows8enhancementsspanwindows8-enhancements"></a><span id="windows_8_enhancements"></span><span id="WINDOWS_8_ENHANCEMENTS"></span>Windows 8 的增强功能


本部分仅适用于 Windows 8 及更高版本、 和 Windows Server 2012 及更高版本。

您可以实现您的 OpenGL 可安装的客户端驱动程序 (ICD) 以用于 Windows 8 提供的以下 OpenGL 增强功能：

### <a name="span-idcontrollingresourceaccesswithmutexesspanspan-idcontrollingresourceaccesswithmutexesspanspan-idcontrollingresourceaccesswithmutexesspancontrolling-resource-access-with-mutexes"></a><span id="Controlling_Resource_Access_with_Mutexes_"></span><span id="controlling_resource_access_with_mutexes_"></span><span id="CONTROLLING_RESOURCE_ACCESS_WITH_MUTEXES_"></span>控制资源访问的互斥锁

可以使用这些 OpenGL 互斥体函数和关联结构，以指定要将与键控的互斥体相关联的私有数据时控制对资源的访问：

-   [**D3DKMTAcquireKeyedMutex2**](https://msdn.microsoft.com/library/windows/hardware/hh439340)
-   [**D3DKMTCreateKeyedMutex2**](https://msdn.microsoft.com/library/windows/hardware/hh439345)
-   [**D3DKMT\_ACQUIREKEYEDMUTEX2**](https://msdn.microsoft.com/library/windows/hardware/hh439466)
-   [**D3DKMT\_CREATEKEYEDMUTEX2**](https://msdn.microsoft.com/library/windows/hardware/hh439474)

### <a name="span-idopenglhelperfunctionsspanspan-idopenglhelperfunctionsspanspan-idopenglhelperfunctionsspanopengl-helper-functions"></a><span id="OpenGL_Helper_Functions"></span><span id="opengl_helper_functions"></span><span id="OPENGL_HELPER_FUNCTIONS"></span>OpenGL 帮助器函数

可以使用这些函数和其关联的结构来访问对象和其句柄：

-   [**D3DKMTGetSharedResourceAdapterLuid**](https://msdn.microsoft.com/library/windows/hardware/jj128339)
-   [**D3DKMTOpenAdapterFromLuid**](https://msdn.microsoft.com/library/windows/hardware/hh780247)
-   [**D3DKMTOpenNtHandleFromName**](https://msdn.microsoft.com/library/windows/hardware/hh439409)
-   [**D3DKMTOpenResourceFromNtHandle**](https://msdn.microsoft.com/library/windows/hardware/hh439413)
-   [**D3DKMTOpenSyncObjectFromNtHandle**](https://msdn.microsoft.com/library/windows/hardware/hh780248)
-   [**D3DKMT\_GETSHAREDRESOURCEADAPTERLUID**](https://msdn.microsoft.com/library/windows/hardware/jj128344)
-   [**D3DKMT\_OPENADAPTERFROMLUID**](https://msdn.microsoft.com/library/windows/hardware/hh780267)
-   [**D3DKMT\_OPENNTHANDLEFROMNAME**](https://msdn.microsoft.com/library/windows/hardware/hh406493)
-   [**D3DKMT\_OPENRESOURCEFROMNTHANDLE**](https://msdn.microsoft.com/library/windows/hardware/hh406496)
-   [**D3DKMT\_OPENSYNCOBJECTFROMNTHANDLE**](https://msdn.microsoft.com/library/windows/hardware/hh780268)

 

 





