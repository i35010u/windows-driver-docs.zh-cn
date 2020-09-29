---
title: 从用户模式组件调用反交错 DDI
description: 从用户模式组件调用反交错 DDI
ms.assetid: 3ec18c7e-02dc-4607-b280-3ca1bc5d2839
keywords:
- 调用取消隔行扫描 DDI WDK DirectX VA
- 用户模式组件调用 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5577bc0f66b1b67cfc3f50858e07486f1867c2d
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423904"
---
# <a name="calling-the-deinterlace-ddi-from-a-user-mode-component"></a>从用户模式组件调用反交错 DDI


## <span id="ddk_calling_the_deinterlace_ddi_from_a_user_mode_component_gg"></span><span id="DDK_CALLING_THE_DEINTERLACE_DDI_FROM_A_USER_MODE_COMPONENT_GG"></span>


用户模式组件（如 VMR）启动对取消隔行扫描 DDI 的调用。

为了使 VMR 能够对视频内容进行逐行转换和执行帧速率转换，显示驱动程序必须实现由[**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的成员定义的[运动补偿回调函数](motion-compensation-callbacks.md)。

为了简化驱动程序开发，驱动程序编写人员可以使用运动补偿代码模板并实现 [取消隔行扫描示例函数](sample-functions-for-deinterlacing.md)。 运动补偿模板调用取消隔行扫描示例函数，以对视频内容执行取消隔行扫描和帧速率转换。 有关使用运动补偿模板的详细信息，请参阅 [DIRECTX VA 设备的示例代码](example-code-for-directx-va-devices.md)。

以下步骤说明了 VMR 如何发起对隔行扫描 DDI 的调用：

1.  将 VMR 添加到筛选器图时，它将启动对驱动程序提供的 [*DdMoCompGetGuids*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids) 回调函数的调用，以检索该驱动程序支持的设备的列表。 DD MOTIONCOMPCALLBACKS 结构的 **GetMoCompGuids** 成员 \_ 指向此回调函数。 有关筛选器关系图的详细信息，请参阅 [KS 微型驱动程序体系结构](../stream/ks-minidriver-architecture.md)。

2.  如果隔行扫描容器设备 GUID 存在，VMR 将启动对 [*DdMoCompCreate*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_create) 回调函数的调用，以创建设备的实例。 DD MOTIONCOMPCALLBACKS 的 **CreateMoComp** 成员指向 \_ 回调函数。 在*DdMoCompCreate*调用中，指向容器设备 GUID 的指针是在[**DD \_ CREATEMOCOMPDATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_createmocompdata)结构的**lpGuid**成员中指定的。 容器设备 GUID 定义如下：
    ```cpp
    DEFINE_GUID(DXVA_DeinterlaceContainerDevice, 0x0e85cb93,0x3046,0x4ff0,0xae,0xcc,0xd5,0x8c,0xb5,0xf0,0x35,0xfd);
    ```

3.  若要确定特定输入视频格式的可用取消隔行扫描或帧速率转换模式，VMR 将启动对驱动程序提供的 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数的调用。 [**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)的**RenderMoComp**成员指向回调函数。 在**DdMoCompRender**调用中， *DXVA*) 中定义的**DXVA \_ ProcAmpControlQueryCapsFnCode**常量 (在[**DD \_ dwFunction**](/windows/win32/api/ddrawint/ns-ddrawint-dd_rendermocompdata)结构的**RENDERMOCOMPDATA**成员中进行了设置。 DD RENDERMOCOMPDATA 的 **lpInputData** 成员 \_ 通过指向已完成的 [**DXVA \_ VideoDesc**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc) 结构将输入参数传递给驱动程序。 驱动程序通过 DD RENDERMOCOMPDATA 的 **lpOutputData** 成员返回其输出 \_ ; **lpOutputData** 指向 [**DXVA \_ DeinterlaceQueryAvailableModes**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacequeryavailablemodes) 结构。

    如果驱动程序实现了 [**DeinterlaceQueryAvailableModes**](./dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md) 示例函数， **DdMoCompRender** 回调函数将调用 **DeinterlaceQueryAvailableModes**。

4.  对于驱动程序支持的每个取消隔行扫描模式，VMR 将启动对驱动程序提供的 **DdMoCompRender**回调函数的调用。 在**DdMoCompRender**调用中， *DXVA*) 中定义的**DXVA \_ DeinterlaceQueryModeCapsFnCode**常量 (在 DD dwFunction 的**RENDERMOCOMPDATA**成员中进行了设置 \_ 。 DD RENDERMOCOMPDATA 的 **lpInputData** 成员 \_ 通过指向已完成的 [**DXVA \_ DeinterlaceQueryModeCaps**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacequerymodecaps) 结构将输入参数传递给驱动程序。 驱动程序通过 DD RENDERMOCOMPDATA 的 **lpOutputData** 成员返回其输出 \_ ; **lpOutputData** 指向 [**DXVA \_ DeinterlaceCaps**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps) 结构。

    如果驱动程序实现了 [**DeinterlaceQueryModeCaps**](./dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps.md) 示例函数， **DdMoCompRender** 回调函数将调用 **DeinterlaceQueryModeCaps**。

5.  VMR 确定了特定取消隔行扫描模式的取消隔行扫描功能后 (例如，小明取消隔行扫描) ，它会启动对 [*DdMoCompCreate*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_create) 的调用，以创建取消隔行扫描模式设备的实例 (例如，取消隔行扫描 bob 设备) 。 在 *DdMoCompCreate* 调用中，在 DD CREATEMOCOMPDATA 的 **lpGuid** 成员中指定了指向隔行扫描模式设备 GUID 的指针 \_ 。 逐行扫描 bob 设备 GUID 定义如下：

    ```cpp
    DEFINE_GUID(DXVAp_DeinterlaceBobDevice, 0x335aa36e,0x7884,0x43a4,0x9c,0x91,0x7f,0x87,0xfa,0xf3,0xe3,0x7e);
    ```

    如果驱动程序实现了 [**DeinterlaceOpenStream**](./dxva-deinterlacebobdeviceclass-deinterlaceopenstream.md) 示例函数， [*DdMoCompCreate*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_create) 回调函数将调用 **DeinterlaceOpenStream**。

6.  对于每个取消隔行扫描操作，VMR 启动对驱动程序提供的 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数的调用。 在*DdMoCompRender*调用中， *DXVA*) 中定义的**DXVA \_ ProcAmpControlQueryCapsFnCode**常量 (在 DD dwFunction 的**RENDERMOCOMPDATA**成员中进行了设置 \_ 。 DD RENDERMOCOMPDATA 的 **lpBufferInfo** 成员指向 \_ 一组缓冲区，这些缓冲区描述目标图面和每个输入视频源示例。 DD RENDERMOCOMPDATA 的 **lpInputData** 成员 \_ 通过指向已完成的 [**DXVA \_ DeinterlaceBlt**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlaceblt) 结构将输入参数传递给驱动程序。 驱动程序未返回任何输出;也就是说，DD RENDERMOCOMPDATA 的 **lpOutputData** 成员 \_ 为 **NULL**。

    如果驱动程序实现了 [**DeinterlaceBlt**](./dxva-deinterlacebobdeviceclass-deinterlaceblt.md) 示例函数， **DdMoCompRender** 回调函数将调用 **DeinterlaceBlt**。

7.  对于每个组合取消隔行扫描和子流组合操作，Microsoft Windows Server 2003 SP1 及更高版本和 Windows XP SP2 及更高版本上的 VMR 将启动对驱动程序提供的 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数的调用。 在*DdMoCompRender*调用中， *DXVA*) 中定义的**DXVA \_ DeinterlaceBltExFnCode**常量 (在 DD dwFunction 的**RENDERMOCOMPDATA**成员中进行了设置 \_ 。 DD RENDERMOCOMPDATA 的 **lpBufferInfo** 成员指向一 \_ 组缓冲区，这些缓冲区描述目标图面和每个输入视频源示例的图面。 DD RENDERMOCOMPDATA 的 **lpInputData** 成员 \_ 通过指向已完成的 [**DXVA \_ DeinterlaceBltEx**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex) 结构将输入参数传递给驱动程序。 驱动程序未返回任何输出;也就是说，DD RENDERMOCOMPDATA 的 **lpOutputData** 成员 \_ 为 **NULL**。

    如果驱动程序实现了 [**DeinterlaceBltEx**](./dxva-deinterlacebobdeviceclass-deinterlacebltex.md) 示例函数， **DdMoCompRender** 回调函数将调用 **DeinterlaceBltEx**。

8.  当 VMR 不再需要执行更多的取消隔行扫描操作时，将调用驱动程序提供的 [*DdMoCompDestroy*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy) 回调函数。 DD MOTIONCOMPCALLBACKS 的 **DestroyMoComp** 成员指向 \_ 回调函数。

    如果驱动程序实现了 [**DeinterlaceCloseStream**](./dxva-deinterlacebobdeviceclass-deinterlaceclosestream.md) 示例函数， [*DdMoCompDestroy*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy) 回调函数将调用 **DeinterlaceCloseStream**。

9.  然后，该驱动程序将释放由隔行扫描模式设备使用的所有资源。

 

