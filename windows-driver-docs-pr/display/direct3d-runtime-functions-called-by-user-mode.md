---
title: D3D 调用的用户模式显示驱动程序的运行时函数
description: 本主题引用 Microsoft Direct3D 运行时提供给用户模式显示驱动程序的函数。
ms.assetid: CB6A0314-E410-4865-8833-801BDB24AA25
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: ea18cb642e22bc1845c347c8d1417098739902e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534338"
---
# <a name="direct3d-runtime-functions-called-by-user-mode-display-drivers"></a>Direct3D 调用的用户模式显示驱动程序的运行时函数

本主题引用 Microsoft Direct3D 运行时提供给用户模式显示驱动程序的函数。 其中包括 Direct3D 运行时内核服务访问函数和 Direct3D 的运行时版本 10 和 11 函数。 这些函数是操作系统实现通过 Direct3D 运行时的用户模式下 Direct3D 显示驱动程序接口的一部分。

## <a name="direct3d-runtime-kernel-services-accessing-functions"></a>Direct3D 运行时内核服务访问功能

**Microsoft Direct3D 版本 9**运行时提供指向*特定于适配器*回调函数的成员通过[D3DDDI_ADAPTERCALLBACKS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_adaptercallbacks)结构对用户模式下的调用中显示器驱动程序的[OpenAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_openadapter)函数。 运行时会提供指针，以显示*特定于设备*回调函数的成员通过[D3DDDI_DEVICECALLBACKS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)结构对用户模式显示驱动程序的调用中[CreateDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)函数。 

**Microsoft Direct3D 版本 10**或更高版本的运行时提供的成员通过特定于适配器的回调函数的指针**D3DDDI_ADAPTERCALLBACKS**对用户模式下的调用中的结构显示驱动程序的[OpenAdapter10](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)或 OpenAdapter10_2 函数。 运行时会提供要显示的成员通过特定于设备的回调函数指针**D3DDDI_DEVICECALLBACKS**对用户模式显示驱动程序的调用中的结构[CreateDevice(D3D10)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数。

|函数 | |
|:----|:----|
|[PFND3DDDI_ALLOCATECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)|[PFND3DDDI_CREATECONTEXTVIRTUALCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createcontextvirtualcb)|
|[PFND3DDDI_CREATEHWCONTEXTCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createhwcontextcb)|[PFND3DDDI_CREATEHWQUEUECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createhwqueuecb)|
|[PFND3DDDI_CREATEOVERLAYCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createoverlaycb)|[PFND3DDDI_CREATEPAGINGQUEUECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createpagingqueuecb)|
|[PFND3DDDI_CREATESYNCHRONIZATIONOBJECT2CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createsynchronizationobject2cb)|[PFND3DDDI_CREATESYNCHRONIZATIONOBJECTCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createsynchronizationobjectcb)|
|[PFND3DDDI_DEALLOCATE2CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocate2cb) |[PFND3DDDI_DEALLOCATECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb)|
|[PFND3DDDI_DESTROYCONTEXTCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroycontextcb)|[PFND3DDDI_DESTROYHWCONTEXTCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyhwcontextcb) |
|[PFND3DDDI_DESTROYHWQUEUECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyhwqueuecb) |[PFND3DDDI_DESTROYOVERLAYCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyoverlaycb) |
|[PFND3DDDI_DESTROYPAGINGQUEUECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroypagingqueuecb) |[PFND3DDDI_DESTROYSYNCHRONIZATIONOBJECTCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroysynchronizationobjectcb) |
|[PFND3DDDI_ESCAPECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_escapecb) |[PFND3DDDI_EVICTCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb) |
|[PFND3DDDI_FLIPOVERLAYCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_flipoverlaycb) |[PFND3DDDI_FREEGPUVIRTUALADDRESSCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_freegpuvirtualaddresscb) |
|[PFND3DDDI_GETMULTISAMPLEMETHODLISTCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getmultisamplemethodlistcb) |[PFND3DDDI_GETRESOURCEPRESENTPRIVATEDRIVERDATACB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getresourcepresentprivatedriverdatacb) |
|[PFND3DDDI_LOCK2CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lock2cb) |[PFND3DDDI_LOCKCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb) |
|[PFND3DDDI_LOGUMDMARKERCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_logumdmarkercb) |[PFND3DDDI_MAKERESIDENTCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb) |
|[PFND3DDDI_MAPGPUVIRTUALADDRESSCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_mapgpuvirtualaddresscb) |[PFND3DDDI_OFFERALLOCATIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_offerallocationscb)|
|[PFND3DDDI_OFFERALLOCATIONS2CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_offerallocations2cb) |[PFND3DDDI_PRESENTCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb) |
|[PFND3DDDI_QUERYADAPTERINFOCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb) |[PFND3DDDI_QUERYRESIDENCYCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_queryresidencycb) |
|[PFND3DDDI_RECLAIMALLOCATIONS2CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocations2cb)|[PFND3DDDI_RECLAIMALLOCATIONS3CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocations3cb) |
|[PFND3DDDI_RECLAIMALLOCATIONSCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocationscb)|[PFND3DDDI_RENDERCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb) |
|[PFND3DDDI_RESERVEGPUVIRTUALADDRESSCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_reservegpuvirtualaddresscb) |[PFND3DDDI_SETASYNCCALLBACKSCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setasynccallbackscb) |
|[PFND3DDDI_SETDISPLAYMODECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setdisplaymodecb) |[PFND3DDDI_SETDISPLAYPRIVATEDRIVERFORMATCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setdisplayprivatedriverformatcb) |
|[PFND3DDDI_SETPRIORITYCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setprioritycb) |[PFND3DDDI_SIGNALSYNCHRONIZATIONOBJECT2CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobject2cb) |
|[PFND3DDDI_SIGNALSYNCHRONIZATIONOBJECTCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobjectcb) |[PFND3DDDI_SIGNALSYNCHRONIZATIONOBJECTFROMCPUCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobjectfromcpucb) |
|[PFND3DDDI_SIGNALSYNCHRONIZATIONOBJECTFROMGPU2CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobjectfromgpu2cb) |[PFND3DDDI_SIGNALSYNCHRONIZATIONOBJECTFROMGPUCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobjectfromgpucb) |
|[PFND3DDDI_SUBMITCOMMANDCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_submitcommandcb) |[PFND3DDDI_SUBMITCOMMANDTOHWQUEUECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_submitcommandtohwqueuecb) |
|[PFND3DDDI_SUBMITSIGNALSYNCOBJECTSTOHWQUEUECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_submitsignalsyncobjectstohwqueuecb) |[PFND3DDDI_SUBMITWAITFORSYNCOBJECTSTOHWQUEUECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_submitwaitforsyncobjectstohwqueuecb) |
|[PFND3DDDI_UNLOCK2CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_unlock2cb) |[PFND3DDDI_UNLOCKCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockcb) |
|[PFND3DDDI_UPDATEALLOCATIONPROPERTYCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_updateallocationpropertycb) |[PFND3DDDI_UPDATEOVERLAYCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_updateoverlaycb) |
|[PFND3DDDI_UPDATEGPUVIRTUALADDRESSCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_updategpuvirtualaddresscb) |[PFND3DDDI_WAITFORSYNCHRONIZATIONOBJECT2CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_waitforsynchronizationobject2cb) |
|[PFND3DDDI_WAITFORSYNCHRONIZATIONOBJECTCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_waitforsynchronizationobjectcb) |[PFND3DDDI_WAITFORSYNCHRONIZATIONOBJECTFROMCPUCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_waitforsynchronizationobjectfromcpucb) |
|[PFND3DDDI_WAITFORSYNCHRONIZATIONOBJECTFROMGPUCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_waitforsynchronizationobjectfromgpucb) |[PFND3DWDDM2_0DDI_DECODEJPEG](https://msdn.microsoft.com/library/windows/hardware/dn937733.aspx) |
|[PFND3DWDDM2_0DDI_ENCODEJPEG](https://msdn.microsoft.com/library/windows/hardware/dn937735.aspx) ||

### <a name="direct3d-parameter-structures"></a>Direct3D 参数结构

本部分介绍结构，由 Direct3D 运行时内核服务用于访问函数。 用户模式显示驱动程序将指针传递给这些结构中的运行时函数的参数。


| 结构                                   |                                              |
|:---------------------------------------------|:---------------------------------------------|
| D3DDDI_UPDATEALLOCPROPERTY                   | D3DDDICB_ALLOCATE                            |
| D3DDDICB_CREATECONTEXT                       | D3DDDICB_CREATECONTEXTVIRTUAL                |
| D3DDDICB_CREATEHWCONTEXT                     | D3DDDICB_CREATEHWQUEUE                       |
| D3DDDICB_CREATEOVERLAY                       | D3DDDICB_CREATEPAGINGQUEUE                   |
| D3DDDICB_CREATESYNCHRONIZATIONOBJECT2        | D3DDDICB_CREATESYNCHRONIZATIONOBJECT         |
| D3DDDICB_DESTROYHWCONTEXT                    | D3DDDICB_DESTROYHWQUEUE                      |
| D3DDDICB_DEALLOCATE                          | D3DDDICB_DEALLOCATE2                         |
| D3DDDICB_DESTROYCONTEXT                      | D3DDDICB_DESTROYOVERLAY                      |
| D3DDDICB_DESTROYSYNCHRONIZATIONOBJECT        | D3DDDICB_ESCAPE                              |
| D3DDDICB_EVICT                               | D3DDDICB_FLIPOVERLAY                         |
| D3DDDICB_GETMULTISAMPLEMETHODLIST            | D3DDDICB_LOCK                                |
| D3DDDICB_LOCK2FLAGS                          | D3DDDICB_OFFERALLOCATIONS                    |
| D3DDDICB_PRESENT                             | D3DDDICB_QUERYADAPTERINFO                    |
| D3DDDICB_QUERYRESIDENCY                      | D3DDDICB_RECLAIMALLOCATIONS                  |
| D3DDDICB_RECLAIMALLOCATIONS2                 | D3DDDICB_RENDER                              |
| D3DDDICB_SETDISPLAYMODE                      | D3DDDICB_SETDISPLAYPRIVATEDRIVERFORMAT       |
| D3DDDICB_SETPRIORITY                         | D3DDDICB_SIGNALSYNCHRONIZATIONOBJECT         |
| D3DDDICB_SIGNALSYNCHRONIZATIONOBJECT2        | D3DDDICB_SIGNALSYNCHRONIZATIONOBJECTFROMCPU  |
| D3DDDICB_SIGNALSYNCHRONIZATIONOBJECTFROMGPU  | D3DDDICB_SIGNALSYNCHRONIZATIONOBJECTFROMGPU2 |
| D3DDDICB_SUBMITCOMMAND                       | D3DDDICB_SUBMITCOMMANDFLAGS                  |
| D3DDDICB_SUBMITCOMMANDTOHWQUEUE              | D3DDDICB_SUBMITSIGNALSYNCOBJECTSTOHWQUEUE    |
| D3DDDICB_SUBMITWAITFORSYNCOBJECTSTOHWQUEUE   | D3DDDICB_UNLOCK                              |
| D3DDDICB_UNLOCK2                             | D3DDDICB_UPDATEGPUVIRTUALADDRESS             |
| D3DDDICB_UPDATEOVERLAY                       | D3DDDICB_WAITFORSYNCHRONIZATIONOBJECT        |
| D3DDDICB_WAITFORSYNCHRONIZATIONOBJECT2       | D3DDDICB_WAITFORSYNCHRONIZATIONOBJECTFROMCPU |
| D3DDDICB_WAITFORSYNCHRONIZATIONOBJECTFROMGPU |                                              |

## <a name="direct3d-runtime-version-10-and-later-core-callback-functions"></a>Direct3D 的运行时版本 10 和更高版本的核心回调函数

本部分介绍了 Microsoft Direct3D 10 和更高版本的运行时提供给用户模式显示驱动程序的核心回调函数。 运行时会提供核心的成员通过回调函数的指针[D3D10DDI_CORELAYER_DEVICECALLBACKS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddi_corelayer_devicecallbacks)对用户模式显示驱动程序的调用中的结构[CreateDevice(D3D10)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数。

### <a name="direct3d-runtime-version-10-control-callback-functions"></a>Direct3D 10 的运行时版本控制回调函数

下面是 Microsoft Direct3D 10 和更高版本的运行时提供给用户模式显示驱动程序的控制回调函数的列表。

| | |
|:---|:---|
|[PFND3D10DDI_DISABLE_DEFERRED_STAGING_RESOURCE_DESTRUCTION_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_disable_deferred_staging_resource_destruction_cb) |[PFND3D10DDI_SETERROR_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb) |


### <a name="direct3d-runtime-version-10-state-refresh-callback-functions"></a>Direct3D 10 的运行时版本状态刷新回调函数

在本部分中的参考页介绍了 Microsoft Direct3D 10 运行时提供给用户模式显示驱动程序的状态刷新回调函数。 

Direct3D 10 运行时缓存的应用程序的当前绑定的对象，因为运行时还会缓存在当前绑定的状态对象的用户模式显示驱动程序具有较低的开销。 对于每个调用的用户模式显示驱动程序将向状态刷新回调函数，运行时返回到调用代码驱动程序中之前在同一执行线程中将相应驱动程序状态函数调用 Direct3D 10。 若要提高性能，状态刷新回调函数不执行任何参数验证。 

想要开发无状态的驱动程序或构建命令缓冲区前导码数据时，状态刷新回调函数非常有用。 状态刷新回调函数还允许用户模式显示驱动程序能够受益于 Direct3D 10 运行时维护的高水印。 高水印指示无法为非 NULL; 的最大槽索引因此，高水印经过这种段时提高遍历。

| | |
|:---|:---|
| [PFND3D10DDI_STATE_GS_CONSTBUF_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_gs_constbuf_cb) | [PFND3D10DDI_STATE_GS_SAMPLER_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_gs_sampler_cb) |
|[PFND3D10DDI_STATE_GS_SHADER_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_gs_shader_cb) |[PFND3D10DDI_STATE_GS_SRV_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_gs_srv_cb) |
|[PFND3D10DDI_STATE_IA_INDEXBUF_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_ia_indexbuf_cb) |[PFND3D10DDI_STATE_IA_INPUTLAYOUT_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_ia_inputlayout_cb)|
|[PFND3D10DDI_STATE_IA_PRIMITIVE_TOPOLOGY_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_ia_primitive_topology_cb) |[PFND3D10DDI_STATE_IA_VERTEXBUF_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_ia_vertexbuf_cb)|
|[PFND3D10DDI_STATE_OM_BLENDSTATE_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_om_blendstate_cb)|[PFND3D10DDI_STATE_OM_DEPTHSTATE_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_om_depthstate_cb) |
|[PFND3D10DDI_STATE_OM_RENDERTARGETS_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_om_rendertargets_cb) |[PFND3D10DDI_STATE_PS_CONSTBUF_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_ps_constbuf_cb) |
|[PFND3D10DDI_STATE_PS_SAMPLER_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_ps_sampler_cb) |[PFND3D10DDI_STATE_PS_SHADER_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_ps_shader_cb) |
|[PFND3D10DDI_STATE_PS_SRV_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_ps_srv_cb) |[PFND3D10DDI_STATE_RS_RASTSTATE_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_rs_raststate_cb) |
|[PFND3D10DDI_STATE_RS_SCISSOR_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_rs_scissor_cb) |[PFND3D10DDI_STATE_RS_VIEWPORTS_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_rs_viewports_cb) |
|[PFND3D10DDI_STATE_SO_TARGETS_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_so_targets_cb) |[PFND3D10DDI_STATE_TEXTFILTERSIZE_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_textfiltersize_cb) |
|[PFND3D10DDI_STATE_VS_CONSTBUF_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_vs_constbuf_cb) |[PFND3D10DDI_STATE_VS_SAMPLER_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_vs_sampler_cb) |
|[PFND3D10DDI_STATE_VS_SHADER_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_vs_shader_cb) |[PFND3D10DDI_STATE_VS_SRV_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_vs_srv_cb) |

## <a name="direct3d-runtime-version-10-kernel-services-accessing-functions"></a>Direct3D 10 的运行时版本内核的服务访问功能

本部分介绍内核服务访问 Microsoft Direct3D 10 运行时的 DirectX 图形基础结构 (DXGI) 组件提供给用户模式显示驱动程序的功能。 DXGI 提供指向内核服务访问的成员函数[DXGI_DDI_BASE_CALLBACKS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_callbacks)对用户模式显示驱动程序的调用中的结构[CreateDevice(D3D10)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数.

## <a name="direct3d-runtime-version-11-functions"></a>Direct3D 11 的运行时版本函数

本部分介绍了 Microsoft Direct3D 11 和更高版本的运行时提供给用户模式显示驱动程序的核心回调函数。 运行时会提供核心的成员通过回调函数的指针[D3D11DDI_CORELAYER_DEVICECALLBACKS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddi_corelayer_devicecallbacks)中对用户模式显示驱动程序的 CreateDevice(D3D10) 函数的调用的结构。


### <a name="direct3d-runtime-version-11-control-callback-functions"></a>Direct3D 11 的运行时版本控制回调函数

本部分介绍了 Microsoft Direct3D 11 和更高版本的运行时提供给用户模式显示驱动程序的控制回调函数。

[PFND3D11DDI_PERFORM_AMORTIZED_PROCESSING_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb)

### <a name="direct3d-runtime-version-11-state-refresh-callback-functions"></a>Direct3D 11 的运行时版本状态刷新回调函数

本部分介绍 Microsoft Direct3D 版本 11 和更高版本的运行时提供给用户模式显示驱动程序的状态刷新回调函数。 

Direct3D 11 运行时缓存的应用程序的当前绑定的对象，因为运行时还会缓存在当前绑定的状态对象的用户模式显示驱动程序具有较低的开销。 对于每个调用的用户模式显示驱动程序将向状态刷新回调函数，运行时返回到调用代码驱动程序中之前在同一执行线程中将相应驱动程序状态函数调用 Direct3D 11。 若要提高性能，状态刷新回调函数不执行任何参数验证。 

当您尝试开发无状态的驱动程序或构建命令缓冲区前导码数据时，状态刷新回调函数很有用。 状态刷新回调函数还允许用户模式显示驱动程序能够受益于 Direct3D 11 运行时维护的高水印。 高水印指示无法为非 NULL; 的最大槽索引因此，高水印经过这种段时提高遍历。

| | |
|:---|:---|
| [PFND3D11DDI_STATE_CS_CONSTBUF_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_state_cs_constbuf_cb) | [PFND3D11DDI_STATE_CS_SAMPLER_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_state_cs_sampler_cb) |
| [PFND3D11DDI_STATE_CS_SHADER_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_state_cs_shader_cb) | [PFND3D11DDI_STATE_CS_SRV_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_state_cs_srv_cb) |
| [PFND3D11DDI_STATE_CS_UAV_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_state_cs_uav_cb) | [PFND3D11DDI_STATE_DS_CONSTBUF_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_state_ds_constbuf_cb) |
| [PFND3D11DDI_STATE_DS_SAMPLER_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_state_ds_sampler_cb) | [PFND3D11DDI_STATE_DS_SHADER_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_state_ds_shader_cb) |
| [PFND3D11DDI_STATE_DS_SRV_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_state_ds_srv_cb) | [PFND3D11DDI_STATE_HS_CONSTBUF_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_state_hs_constbuf_cb) |
| [PFND3D11DDI_STATE_HS_SAMPLER_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_state_hs_sampler_cb) | [PFND3D11DDI_STATE_HS_SHADER_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_state_hs_shader_cb) |
| [PFND3D11DDI_STATE_HS_SRV_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_state_hs_srv_cb) |  |


## <a name="direct3d-runtime-version-12-and-later-functions"></a>Direct3D 12 及更高版本的运行时版本函数

在本部分中的参考页介绍了 Microsoft Direct3D 12 和更高版本的运行时提供给用户模式显示驱动程序的核心回调函数。 

| | |
|:---|:---|
| [PFND3D12DDI_WRITEBUFFERIMMEDIATE_0032](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_writebufferimmediate_0032) | [PFND3D12DDI_VIDEO_PROCESS_FRAME_0032](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_video_process_frame_0032) |
| [PFND3D12DDI_VIDEO_DECODE_FRAME_0032](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_video_decode_frame_0032) | PFND3D12DDI_VIDEO_DECODE_FRAME_0030 |
| [PFND3D12DDI_TRANSFORMENCRYPTEDDATA_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_transformencrypteddata_0030) | [PFND3D12DDI_SETVIEWINSTANCEMASK_0033](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_setviewinstancemask_0033) |
| [PFND3D12DDI_SETPROTECTEDRESOURCESESSION_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_setprotectedresourcesession_0030) | [PFND3D12DDI_OPENPROTECTEDRESOURCESESSION_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_openprotectedresourcesession_0030) |
| [PFND3D12DDI_OPENCRYPTOSESSIONPOLICY_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_opencryptosessionpolicy_0030) | [PFND3D12DDI_OPENCRYPTOSESSION_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_opencryptosession_0030) |
| [PFND3D12DDI_GETKEYBASEDATA_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_getkeybasedata_0030) | [PFND3D12DDI_DESTROYVIDEODECODERHEAP_0032](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_destroyvideodecoderheap_0032) |
| [PFND3D12DDI_DESTROYPROTECTEDRESOURCESESSION_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_destroyprotectedresourcesession_0030) | [PFND3D12DDI_DESTROYCRYPTOSESSIONPOLICY_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_destroycryptosessionpolicy_0030) |
| [PFND3D12DDI_DESTROYCRYPTOSESSION_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_destroycryptosession_0030) | [PFND3D12DDI_CREATEVIDEOPROCESSOR_0032](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_createvideoprocessor_0032) |
| [PFND3D12DDI_CREATEVIDEODECODERHEAP_0033](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_createvideodecoderheap_0033) | PFND3D12DDI_CREATEVIDEODECODERHEAP_0032 |
| [PFND3D12DDI_CREATEVIDEODECODER_0032](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_createvideodecoder_0032) | [PFND3D12DDI_CREATEPROTECTEDRESOURCESESSION_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_createprotectedresourcesession_0030) |
| [PFND3D12DDI_CREATEHEAPANDRESOURCE_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_createheapandresource_0030) | [PFND3D12DDI_CREATECRYPTOSESSIONPOLICY_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_createcryptosessionpolicy_0030) |
| [PFND3D12DDI_CREATECRYPTOSESSION_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_createcryptosession_0030) | [PFND3D12DDI_CREATE_PROTECTED_SESSION_CB_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_create_protected_session_cb_0030) |
| [PFND3D12DDI_CREATE_PIPELINE_STATE_0033](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_create_pipeline_state_0033) | [PFND3D12DDI_CALCPRIVATEVIDEOPROCESSORSIZE_0032](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_calcprivatevideoprocessorsize_0032) |
| [PFND3D12DDI_CALCPRIVATEVIDEODECODERSIZE_0032](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_calcprivatevideodecodersize_0032) | [PFND3D12DDI_CALCPRIVATEVIDEODECODERHEAPSIZE_0033](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_calcprivatevideodecoderheapsize_0033) |
| PFND3D12DDI_CALCPRIVATEVIDEODECODERHEAPSIZE_0032 | [PFND3D12DDI_CALCPRIVATEPROTECTEDRESOURCESESSIONSIZE_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_calcprivateprotectedresourcesessionsize_0030) |
| [PFND3D12DDI_CALCPRIVATEOPENEDPROTECTEDRESOURCESESSIONSIZE_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_calcprivateopenedprotectedresourcesessionsize_0030) | [PFND3D12DDI_CALCPRIVATEOPENEDCRYPTOSESSIONSIZE_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_calcprivateopenedcryptosessionsize_0030) |
| [PFND3D12DDI_CALCPRIVATEOPENEDCRYPTOSESSIONPOLICYSIZE_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_calcprivateopenedcryptosessionpolicysize_0030) | [PFND3D12DDI_CALCPRIVATECRYPTOSESSIONSIZE_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_calcprivatecryptosessionsize_0030) |
| [PFND3D12DDI_CALCPRIVATECRYPTOSESSIONPOLICYSIZE_0030](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_calcprivatecryptosessionpolicysize_0030) | [PFND3D12DDI_CALC_PRIVATE_PIPELINE_STATE_SIZE_0033](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_calc_private_pipeline_state_size_0033) |
| [PFND3D12DDI_CREATEVIDEOPROCESSOR_0043](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_createvideoprocessor_0043) | [PFND3D12DDI_DESTROYVIDEODECODERHEAP_0032](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_destroyvideodecoderheap_0032) |
| [PFND3D12DDI_CREATEVIDEODECODERHEAP_0033](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_createvideodecoderheap_0033) | PFND3D12DDI_CALCPRIVATEVIDEODECODERHEAP |
| [PFND3D12DDI_DESTROYVIDEODECODER_0021](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_destroyvideodecoder_0021) | PFND3D12DDI_CALCPRIVATEVIDEODECODER |
| [PFND3D12DDI_ALLOCATE_CB_0022](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_allocate_cb_0022) | [PFND3D12DDI_BEGIN_END_QUERY_0003](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_begin_end_query_0003) |
| [PFND3D12DDI_CALCPRIVATECOMMANDQUEUESIZE_0023](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_calcprivatecommandqueuesize_0023) | [PFND3D12DDI_CALCPRIVATEVIDEODECODERSIZE_0032](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_calcprivatevideodecodersize_0032) |
| [PFND3D12DDI_CALCPRIVATEVIDEOPROCESSORSIZE_0032](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_calcprivatevideoprocessorsize_0032) | [PFND3D12DDI_CHECKRESOURCEALLOCATIONINFO_0022](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_checkresourceallocationinfo_0022) |
| [PFND3D12DDI_CHECKEXISITINGRESOURCEALLOCATIONINFO_0022](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_checkexisitingresourceallocationinfo_0022) | [PFND3D12DDI_CREATE_PIPELINE_STATE_0021](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_create_pipeline_state_0021) |
|[PFND3D12DDI_CREATECOMMANDQUEUE_0023](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_createcommandqueue_0023)|[PFND3D12DDI_CREATEVIDEODECODER_0032](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_createvideodecoder_0032) |
|[PFND3D12DDI_CREATEVIDEOPROCESSOR_0032](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_createvideoprocessor_0032)|[PFND3D12DDI_DEALLOCATE_CB_0022](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_deallocate_cb_0022)|
|[PFND3D12DDI_DESTROYVIDEODECODER_0021](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_destroyvideodecoder_0021)|[PFND3D12DDI_DESTROYVIDEOPROCESSOR_0021](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_destroyvideoprocessor_0021)|
|PFND3D12DDI_GETPAGEABLESIZE|[PFND3D12DDI_RESOLVE_QUERY_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_resolve_query_data)|
|[PFND3D12DDI_RESOURCEBARRIER_0022](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_resourcebarrier_0022)|[PFND3D12DDI_SET_EXTENDED_FEATURE_CALLBACKS_0021](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_set_extended_feature_callbacks_0021)|
|[PFND3D12DDI_SET_PREDICATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_set_predication)|[PFND3D12DDI_SHADERCACHEGETVALUE_CB_0021](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_shadercachegetvalue_cb_0021)|
|[PFND3D12DDI_SHADERCACHESTOREVALUE_CB_0021](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_shadercachestorevalue_cb_0021)|[PFND3D12DDI_VIDEO_DECODE_FRAME](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_video_decode_frame_0032)|
|PFND3D12DDI_VIDEO_DECODER_TRIM_ALLOCATIONS|PFND3D12DDI_VIDEO_GET_DECODE_BITSTREAM_ENCRYPTION_SCHEME_COUNT|
|PFND3D12DDI_VIDEO_GET_DECODE_FORMAT_COUNT|PFND3D12DDI_VIDEO_GET_DECODE_PROFILE_COUNT|
|[PFND3D12DDI_VIDEO_GETCAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_video_getcaps)|[PFND3D12DDI_VIDEO_PROCESS_FRAME_0032](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_video_process_frame_0032)|
|PFND3D12DDI_VIDEO_PROCESSOR_TRIM_ALLOCATIONS|[PFND3DWDDM2_0DDI_GETRESOURCELAYOUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3dwddm2_0ddi_getresourcelayout)|
|[PFND3DWDDM2_2DDI_CALCPRIVATE_SHADERCACHE_SESSION_SIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3dwddm2_2ddi_calcprivate_shadercache_session_size)|[PFND3DWDDM2_2DDI_CREATE_SHADERCACHE_SESSION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3dwddm2_2ddi_create_shadercache_session)|
|[PFND3DWDDM2_2DDI_DESTROY_SHADERCACHE_SESSION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3dwddm2_2ddi_destroy_shadercache_session)|[PFND3DWDDM2_2DDI_RELOCATEDEVICEFUNCS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3dwddm2_2ddi_relocatedevicefuncs)|
|[PFND3DWDDM2_2DDI_SET_SHADERCACHE_SESSION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3dwddm2_2ddi_set_shadercache_session)|[PFND3DWDDM2_2DDI_SHADERCACHE_ADDREF_RELEASE_CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3dwddm2_2ddi_shadercache_addref_release_cb)|
|PFND3DWDDM2_2DDI_SHADERCACHE_GET_VALUE|[PFND3DWDDM2_2DDI_SHADERCACHE_STORE_VALUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3dwddm2_2ddi_shadercache_store_value_cb)|

## <a name="see-also"></a>另请参阅

[支持 DXGI DDI](supporting-the-dxgi-ddi.md)

[Multiplane 覆盖的支持](multiplane-overlay-support.md)

[由用户模式显示驱动程序实现的 Direct3D 函数](direct3d-functions-implemented-by-user-mode.md)

[Direct3D 呈现性能改进](direct3d-rendering-performance-improvements.md)
