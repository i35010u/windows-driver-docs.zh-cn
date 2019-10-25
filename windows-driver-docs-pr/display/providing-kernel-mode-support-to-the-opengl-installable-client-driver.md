---
title: OpenGL 可安装客户端驱动程序的内核模式支持
description: 为 OpenGL 可安装客户端驱动程序提供内核模式支持
ms.assetid: 1871594a-ca4d-4a3c-bf12-bbf80fecefe9
keywords:
- OpenGL ICD WDK 显示
- 内核模式 OpenGL ICD WDK 显示
- ICD WDK 显示
- 可安装客户端驱动程序 WDK 显示
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 1e0e6ed3a8e1acf684e7233fbb0a5e38cc14de9f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829672"
---
# <a name="kernel-mode-support-to-the-opengl-installable-client-driver"></a>OpenGL 可安装客户端驱动程序的内核模式支持


OpenGL 可安装客户端驱动程序（ICD）可以获得与将内核模式服务作为[Direct3D 用户模式显示驱动程序](initializing-communication-with-the-direct3d-user-mode-display-driver.md)调用的相同级别的支持。 但是，不是通过回调函数（如 Microsoft Direct3D 运行时通过[**D3DDDIARG\_OPENADAPTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_openadapter)结构的**pAdapterCallbacks**成员提供）和**pCallbacks** [**D3DDDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_createdevice)结构的成员，则 opengl ICD 必须加载 Gdi32 并初始化使用[OpenGL 内核模式访问函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)，如下面的示例代码所示。 此代码不实现[OpenGL 中的 Windows 8 增强功能](supporting-opengl-enhancements.md)。

**请注意**，   获取 Opengl ICD 开发工具包的许可证，请联系[opengl 问题](mailto:opengl@microsoft.com)团队。

 

```cpp
#include "d3dkmthk.h"

PFND3DKMT_CREATEALLOCATION pfnKTCreateAllocation = NULL;
PFND3DKMT_DESTROYALLOCATION pfnKTDestroyAllocation = NULL;
PFND3DKMT_SETALLOCATIONPRIORITY pfnKTSetAllocationPriority = NULL;
PFND3DKMT_QUERYALLOCATIONRESIDENCY pfnKTQueryAllocationResidency = NULL;
PFND3DKMT_QUERYRESOURCEINFO pfnKTQueryResourceInfo = NULL;
PFND3DKMT_OPENRESOURCE pfnKTOpenResource = NULL;
PFND3DKMT_CREATEDEVICE pfnKTCreateDevice = NULL;
PFND3DKMT_DESTROYDEVICE pfnKTDestroyDevice = NULL;
PFND3DKMT_QUERYADAPTERINFO pfnKTQueryAdapterInfo = NULL;
PFND3DKMT_LOCK pfnKTLock = NULL;
PFND3DKMT_UNLOCK pfnKTUnlock = NULL;
PFND3DKMT_GETDISPLAYMODELIST pfnKTGetDisplayModeList = NULL;
PFND3DKMT_SETDISPLAYMODE pfnKTSetDisplayMode = NULL;
PFND3DKMT_GETMULTISAMPLEMETHODLIST pfnKTGetMultisampleMethodList = NULL;
PFND3DKMT_PRESENT pfnKTPresent = NULL;
PFND3DKMT_RENDER pfnKTRender = NULL;
PFND3DKMT_OPENADAPTERFROMHDC pfnKTOpenAdapterFromHdc = NULL;
PFND3DKMT_OPENADAPTERFROMDEVICENAME pfnKTOpenAdapterFromDeviceName = NULL;
PFND3DKMT_CLOSEADAPTER pfnKTCloseAdapter = NULL;
PFND3DKMT_GETSHAREDPRIMARYHANDLE pfnKTGetSharedPrimaryHandle = NULL;
PFND3DKMT_ESCAPE pfnKTEscape = NULL;
PFND3DKMT_SETVIDPNSOURCEOWNER pfnKTSetVidPnSourceOwner = NULL;
 
PFND3DKMT_CREATEOVERLAY pfnKTCreateOverlay = NULL;
PFND3DKMT_UPDATEOVERLAY pfnKTUpdateOverlay = NULL;
PFND3DKMT_FLIPOVERLAY pfnKTFlipOverlay = NULL;
PFND3DKMT_DESTROYOVERLAY pfnKTDestroyOverlay = NULL;
PFND3DKMT_WAITFORVERTICALBLANKEVENT pfnKTWaitForVerticalBlankEvent = NULL;
PFND3DKMT_SETGAMMARAMP pfnKTSetGammaRamp = NULL;
PFND3DKMT_GETDEVICESTATE pfnKTGetDeviceState = NULL;
PFND3DKMT_CREATEDCFROMMEMORY pfnKTCreateDCFromMemory = NULL;
PFND3DKMT_DESTROYDCFROMMEMORY pfnKTDestroyDCFromMemory = NULL;
PFND3DKMT_SETCONTEXTSCHEDULINGPRIORITY pfnKTSetContextSchedulingPriority = NULL;
PFND3DKMT_GETCONTEXTSCHEDULINGPRIORITY pfnKTGetContextSchedulingPriority = NULL;
PFND3DKMT_SETPROCESSSCHEDULINGPRIORITYCLASS pfnKTSetProcessSchedulingPriorityClass = NULL;
PFND3DKMT_GETPROCESSSCHEDULINGPRIORITYCLASS pfnKTGetProcessSchedulingPriorityClass = NULL;
PFND3DKMT_RELEASEPROCESSVIDPNSOURCEOWNERS pfnKTReleaseProcessVidPnSourceOwners = NULL;
PFND3DKMT_GETSCANLINE pfnKTGetScanLine = NULL;
PFND3DKMT_POLLDISPLAYCHILDREN pfnKTPollDisplayChildren = NULL;
PFND3DKMT_SETQUEUEDLIMIT pfnKTSetQueuedLimit = NULL;
PFND3DKMT_INVALIDATEACTIVEVIDPN pfnKTInvalidateActiveVidPn = NULL;
PFND3DKMT_CHECKOCCLUSION pfnKTCheckOcclusion = NULL;
PFND3DKMT_GETPRESENTHISTORY pfnKTGetPresentHistory = NULL;
PFND3DKMT_CREATECONTEXT pfnKTCreateContext = NULL;
PFND3DKMT_DESTROYCONTEXT pfnKTDestroyContext = NULL;
PFND3DKMT_CREATESYNCHRONIZATIONOBJECT pfnKTCreateSynchronizationObject = NULL;
PFND3DKMT_DESTROYSYNCHRONIZATIONOBJECT pfnKTDestroySynchronizationObject = NULL;
PFND3DKMT_WAITFORSYNCHRONIZATIONOBJECT pfnKTWaitForSynchronizationObject = NULL;
PFND3DKMT_SIGNALSYNCHRONIZATIONOBJECT pfnKTSignalSynchronizationObject = NULL;
PFND3DKMT_CHECKMONITORPOWERSTATE pfnKTCheckMonitorPowerState = NULL;
PFND3DKMT_OPENADAPTERFROMGDIDISPLAYNAME pfnKTOpenAdapterFromGDIDisplayName = NULL;
PFND3DKMT_CHECKEXCLUSIVEOWNERSHIP pfnKTCheckExclusiveOwnership = NULL;
PFND3DKMT_SETDISPLAYPRIVATEDRIVERFORMAT pfnKTSetDisplayPrivateDriverFormat = NULL;
PFND3DKMT_SHAREDPRIMARYLOCKNOTIFICATION pfnKTSharedPrimaryLockNotification = NULL;
PFND3DKMT_SHAREDPRIMARYUNLOCKNOTIFICATION pfnKTSharedPrimaryUnLockNotification = NULL;

HRESULT InitKernelTHunks()
{
    HINSTANCE hInst = NULL;

    hInst = LoadLibrary( "gdi32.dll" );
    if (hInst == NULL) {
        return E_FAIL;
    }

    pfnKTCreateAllocation = (PFND3DKMT_CREATEALLOCATION)
         GetProcAddress((HMODULE)hInst, "D3DKMTCreateAllocation" );

    pfnKTQueryResourceInfo = (PFND3DKMT_QUERYRESOURCEINFO)
         GetProcAddress((HMODULE)hInst, "D3DKMTQueryResourceInfo" );

    pfnKTOpenResource = (PFND3DKMT_OPENRESOURCE)
         GetProcAddress((HMODULE)hInst, "D3DKMTCreateAllocation" );

    pfnKTDestroyAllocation = (PFND3DKMT_DESTROYALLOCATION)
         GetProcAddress((HMODULE)hInst, "D3DKMTDestroyAllocation" );

    pfnKTSetAllocationPriority = (PFND3DKMT_SETALLOCATIONPRIORITY)
         GetProcAddress((HMODULE)hInst, "D3DKMTSetAllocationPriority" );

    pfnKTQueryAllocationResidency = (PFND3DKMT_QUERYALLOCATIONRESIDENCY)
         GetProcAddress((HMODULE)hInst, "D3DKMTQueryAllocationResidency" );

    pfnKTCreateDevice = (PFND3DKMT_CREATEDEVICE)
         GetProcAddress((HMODULE)hInst, "D3DKMTCreateDevice" );

    pfnKTDestroyDevice = (PFND3DKMT_DESTROYDEVICE)
         GetProcAddress((HMODULE)hInst, "D3DKMTDestroyDevice" );

    pfnKTQueryAdapterInfo = (PFND3DKMT_QUERYADAPTERINFO)
         GetProcAddress((HMODULE)hInst, "D3DKMTQueryAdapterInfo" );

    pfnKTLock = (PFND3DKMT_LOCK)
         GetProcAddress((HMODULE)hInst, "D3DKMTLock" );

    pfnKTUnlock = (PFND3DKMT_UNLOCK)
         GetProcAddress((HMODULE)hInst, "D3DKMTUnlock" );

    pfnKTGetDisplayModeList = (PFND3DKMT_GETDISPLAYMODELIST)
         GetProcAddress((HMODULE)hInst, "D3DKMTGetDisplayModeList" );

    pfnKTSetDisplayMode = (PFND3DKMT_SETDISPLAYMODE)
         GetProcAddress((HMODULE)hInst, "D3DKMTSetDisplayMode" );

    pfnKTGetMultisampleMethodList = (PFND3DKMT_GETDISPLAYMODELIST)
         GetProcAddress((HMODULE)hInst, "D3DKMTGetMultisampleMethodList" );

    pfnKTPresent = (PFND3DKMT_PRESENT)
         GetProcAddress((HMODULE)hInst, "D3DKMTPresent" );

    pfnKTRender = (PFND3DKMT_RENDER)
         GetProcAddress((HMODULE)hInst, "D3DKMTRender" );

    pfnKTOpenAdapterFromHdc = (PFND3DKMT_OPENADAPTERFROMHDC)
         GetProcAddress((HMODULE)hInst, "D3DKMTOpenAdapterFromHdc" );

    pfnKTOpenAdapterFromDeviceName = (PFND3DKMT_OPENADAPTERFROMDEVICENAME)
         GetProcAddress((HMODULE)hInst, "D3DKMTOpenAdapterFromDeviceName" );

    pfnKTCloseAdapter = (PFND3DKMT_CLOSEADAPTER)
         GetProcAddress((HMODULE)hInst, "D3DKMTCloseAdapter" );

    pfnKTGetSharedPrimaryHandle = (PFND3DKMT_GETSHAREDPRIMARYHANDLE)
         GetProcAddress((HMODULE)hInst, "D3DKMTGetSharedPrimaryHandle" );

    pfnKTEscape = (PFND3DKMT_ESCAPE)
         GetProcAddress((HMODULE)hInst, "D3DKMTEscape" );
 
    pfnKTSetVidPnSourceOwner = (PFND3DKMT_SETVIDPNSOURCEOWNER)
         GetProcAddress((HMODULE)hInst, "D3DKMTSetVidPnSourceOwner" );

    pfnKTReleaseProcessVidPnSourceOwners = (PFND3DKMT_RELEASEPROCESSVIDPNSOURCEOWNERS)
         GetProcAddress((HMODULE)hInst, "D3DKMTReleaseProcessVidPnSourceOwners" );

    pfnKTCreateOverlay = (PFND3DKMT_CREATEOVERLAY)
         GetProcAddress((HMODULE)hInst, "D3DKMTCreateOverlay" );

    pfnKTUpdateOverlay = (PFND3DKMT_UPDATEOVERLAY)
         GetProcAddress((HMODULE)hInst, "D3DKMTUpdateOverlay" );

    pfnKTFlipOverlay = (PFND3DKMT_FLIPOVERLAY)
         GetProcAddress((HMODULE)hInst, "D3DKMTFlipOverlay" );

    pfnKTDestroyOverlay = (PFND3DKMT_DESTROYOVERLAY)
         GetProcAddress((HMODULE)hInst, "D3DKMTDestroyOverlay" );

    pfnKTWaitForVerticalBlankEvent = (PFND3DKMT_WAITFORVERTICALBLANKEVENT)
         GetProcAddress((HMODULE)hInst, "D3DKMTWaitForVerticalBlankEvent" );

    pfnKTSetGammaRamp = (PFND3DKMT_SETGAMMARAMP)
         GetProcAddress((HMODULE)hInst, "D3DKMTSetGammaRamp" );

    pfnKTGetDeviceState = (PFND3DKMT_GETDEVICESTATE)
         GetProcAddress((HMODULE)hInst, "D3DKMTGetDeviceState" );

    pfnKTCreateDCFromMemory = (PFND3DKMT_CREATEDCFROMMEMORY)
         GetProcAddress((HMODULE)hInst, "D3DKMTCreateDCFromMemory" );

    pfnKTDestroyDCFromMemory = (PFND3DKMT_DESTROYDCFROMMEMORY)
         GetProcAddress((HMODULE)hInst, "D3DKMTDestroyDCFromMemory" );

    pfnKTSetContextSchedulingPriority = (PFND3DKMT_SETCONTEXTSCHEDULINGPRIORITY)
         GetProcAddress((HMODULE)hInst, "D3DKMTSetContextSchedulingPriority" );

    pfnKTGetContextSchedulingPriority = (PFND3DKMT_GETCONTEXTSCHEDULINGPRIORITY)
         GetProcAddress((HMODULE)hInst, "D3DKMTGetContextSchedulingPriority" );

    pfnKTSetProcessSchedulingPriorityClass = (PFND3DKMT_SETPROCESSSCHEDULINGPRIORITYCLASS)
         GetProcAddress((HMODULE)hInst, "D3DKMTSetProcessSchedulingPriorityClass" );

    pfnKTGetProcessSchedulingPriorityClass = (PFND3DKMT_GETPROCESSSCHEDULINGPRIORITYCLASS)
         GetProcAddress((HMODULE)hInst, "D3DKMTGetProcessSchedulingPriorityClass" );

    pfnKTGetScanLine = (PFND3DKMT_GETSCANLINE)
         GetProcAddress((HMODULE)hInst, "D3DKMTGetScanLine" );

    pfnKTSetQueuedLimit = (PFND3DKMT_SETQUEUEDLIMIT)
         GetProcAddress((HMODULE)hInst, "D3DKMTSetQueuedLimit" );

    pfnKTPollDisplayChildren = (PFND3DKMT_POLLDISPLAYCHILDREN)
         GetProcAddress((HMODULE)hInst, "D3DKMTPollDisplayChildren" );

    pfnKTInvalidateActiveVidPn = (PFND3DKMT_INVALIDATEACTIVEVIDPN)
         GetProcAddress((HMODULE)hInst, "D3DKMTInvalidateActiveVidPn" );

    pfnKTCheckOcclusion = (PFND3DKMT_CHECKOCCLUSION)
         GetProcAddress((HMODULE)hInst, "D3DKMTCheckOcclusion" );

    pfnKTGetPresentHistory = (PFND3DKMT_GETPRESENTHISTORY)
         GetProcAddress((HMODULE)hInst, "D3DKMTGetPresentHistory" );

    pfnKTCreateContext = (PFND3DKMT_CREATECONTEXT)
         GetProcAddress((HMODULE)hInst, "D3DKMTCreateContext" );

    pfnKTDestroyContext = (PFND3DKMT_DESTROYCONTEXT)
         GetProcAddress((HMODULE)hInst, "D3DKMTDestroyContext" );

    pfnKTCreateSynchronizationObject = (PFND3DKMT_CREATESYNCHRONIZATIONOBJECT)
         GetProcAddress((HMODULE)hInst, "D3DKMTCreateSynchronizationObject" );

    pfnKTDestroySynchronizationObject = (PFND3DKMT_DESTROYSYNCHRONIZATIONOBJECT)
         GetProcAddress((HMODULE)hInst, "D3DKMTDestroySynchronizationObject" );

    pfnKTWaitForSynchronizationObject = (PFND3DKMT_WAITFORSYNCHRONIZATIONOBJECT)
         GetProcAddress((HMODULE)hInst, "D3DKMTWaitForSynchronizationObject" );

    pfnKTSignalSynchronizationObject = (PFND3DKMT_SIGNALSYNCHRONIZATIONOBJECT)
         GetProcAddress((HMODULE)hInst, "D3DKMTSignalSynchronizationObject" );

    pfnKTCheckMonitorPowerState = (PFND3DKMT_CHECKMONITORPOWERSTATE)
         GetProcAddress((HMODULE)hInst, "D3DKMTCheckMonitorPowerState" );

    pfnKTOpenAdapterFromGDIDisplayName = (PFND3DKMT_OPENADAPTERFROMGDIDISPLAYNAME)
         GetProcAddress((HMODULE)hInst, "D3DKMTOpenAdapterFromGdiDisplayName" );

    pfnKTCheckExclusiveOwnership = (PFND3DKMT_CHECKEXCLUSIVEOWNERSHIP)
         GetProcAddress((HMODULE)hInst, "D3DKMTCheckExclusiveOwnership" );

    pfnKTSetDisplayPrivateDriverFormat = (PFND3DKMT_SETDISPLAYPRIVATEDRIVERFORMAT)
         GetProcAddress((HMODULE)hInst, "D3DKMTSetDisplayPrivateDriverFormat" );

    pfnKTSharedPrimaryLockNotification = (PFND3DKMT_SHAREDPRIMARYLOCKNOTIFICATION)
         GetProcAddress((HMODULE)hInst, "D3DKMTSharedPrimaryLockNotification" );

    pfnKTSharedPrimaryUnLockNotification = (PFND3DKMT_SHAREDPRIMARYUNLOCKNOTIFICATION)
         GetProcAddress((HMODULE)hInst, "D3DKMTSharedPrimaryUnLockNotification" );

    if ((pfnKTCreateAllocation == NULL) ||
        (pfnKTQueryResourceInfo == NULL) ||
        (pfnKTOpenResource == NULL) ||
        (pfnKTDestroyAllocation == NULL) ||
        (pfnKTSetAllocationPriority == NULL) ||
        (pfnKTQueryAllocationResidency == NULL) ||
        (pfnKTCreateDevice == NULL) ||
        (pfnKTDestroyDevice == NULL) ||
        (pfnKTQueryAdapterInfo == NULL) ||
        (pfnKTLock == NULL) ||
        (pfnKTUnlock == NULL) ||
        (pfnKTGetDisplayModeList == NULL) ||
        (pfnKTSetDisplayMode == NULL) ||
        (pfnKTGetMultisampleMethodList == NULL) ||
        (pfnKTPresent == NULL) ||
        (pfnKTRender == NULL) ||
        (pfnKTOpenAdapterFromHdc == NULL) ||
        (pfnKTOpenAdapterFromDeviceName == NULL) ||
        (pfnKTCloseAdapter == NULL) ||
        (pfnKTGetSharedPrimaryHandle == NULL) ||
        (pfnKTEscape == NULL) ||
        (pfnKTSetVidPnSourceOwner == NULL) ||
        (pfnKTCreateOverlay == NULL) ||
        (pfnKTUpdateOverlay == NULL) ||
        (pfnKTFlipOverlay == NULL) ||
        (pfnKTDestroyOverlay == NULL) ||
        (pfnKTWaitForVerticalBlankEvent == NULL) ||
        (pfnKTSetGammaRamp == NULL) ||
        (pfnKTGetDeviceState == NULL) ||
        (pfnKTCreateDCFromMemory == NULL) ||
        (pfnKTDestroyDCFromMemory == NULL) ||
        (pfnKTSetContextSchedulingPriority == NULL) ||
        (pfnKTGetContextSchedulingPriority == NULL) ||
        (pfnKTSetProcessSchedulingPriorityClass == NULL) ||
        (pfnKTGetProcessSchedulingPriorityClass == NULL) ||
        (pfnKTReleaseProcessVidPnSourceOwners == NULL) ||
        (pfnKTGetScanLine == NULL) ||
        (pfnKTSetQueuedLimit == NULL) ||
        (pfnKTPollDisplayChildren == NULL) ||
        (pfnKTInvalidateActiveVidPn == NULL) ||
        (pfnKTCheckOcclusion == NULL) ||
        (pfnKTCreateContext == NULL) ||
        (pfnKTDestroyContext == NULL) ||
        (pfnKTCreateSynchronizationObject == NULL) ||
        (pfnKTDestroySynchronizationObject == NULL) ||
        (pfnKTWaitForSynchronizationObject == NULL) ||
        (pfnKTSignalSynchronizationObject == NULL) ||
        (pfnKTCheckMonitorPowerState == NULL) ||
        (pfnKTOpenAdapterFromGDIDisplayName == NULL) ||
        (pfnKTCheckExclusiveOwnership == NULL) ||
        (pfnKTSetDisplayPrivateDriverFormat == NULL) ||
        (pfnKTSharedPrimaryLockNotification == NULL) ||
         (pfnKTSharedPrimaryUnLockNotification == NULL) ||
  (pfnKTGetPresentHistory == NULL))
    {
        return E_FAIL;
    }

    return S_OK;
}
```

 

 





