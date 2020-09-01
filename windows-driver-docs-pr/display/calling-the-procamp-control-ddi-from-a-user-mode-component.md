---
title: 从用户模式组件调用 ProcAmp 控制 DDI
description: 从用户模式组件调用 ProcAmp 控制 DDI
ms.assetid: 1e4e19bb-eb4b-4db6-8947-429a1a414e4a
keywords:
- 调用 ProcAmp 控制 DDI WDK DirectX VA
- 用户模式组件调用 WDK DirectX VA
- ProcAmp WDK DirectX VA，从用户模式组件调用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e24db977b80cde118ba0cacfb5330f235ed065f
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067466"
---
# <a name="calling-the-procamp-control-ddi-from-a-user-mode-component"></a>从用户模式组件调用 ProcAmp 控制 DDI


## <span id="ddk_calling_the_procamp_control_ddi_from_a_user_mode_component_gg"></span><span id="DDK_CALLING_THE_PROCAMP_CONTROL_DDI_FROM_A_USER_MODE_COMPONENT_GG"></span>


用户模式组件（如 VMR）启动对 [ProcAmp 控制 DDI](./procamp-control-ddi.md)的调用。

为了使 VMR 能够访问 ProcAmp 控件功能，显示驱动程序必须实现 [运动补偿回调函数](motion-compensation-callbacks.md)，这些函数是由 [**DD \_ MOTIONCOMPCALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks) 结构的成员定义的。

为了简化驱动程序开发，驱动程序编写器可以使用运动补偿代码模板，并实现 [ProcAmp 控件示例函数](sample-functions-for-procamp-control.md)。 运动补偿模板调用其 ProcAmp 控制示例函数来执行 ProcAmp 控制操作。 有关使用运动补偿模板的详细信息，请参阅 [DIRECTX VA 设备的示例代码](example-code-for-directx-va-devices.md)。

以下步骤说明了 VMR 如何发起对 ProcAmp 控件 DDI 的调用：

1.  将 VMR 添加到筛选器图时，它将启动对驱动程序提供的 [*DdMoCompGetGuids*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids) 回调函数的调用，以检索该驱动程序支持的设备的列表。 DD MOTIONCOMPCALLBACKS 的 **GetMoCompGuids** 成员指向 \_ 此回调函数。 有关筛选器关系图的详细信息，请参阅 [KS 微型驱动程序体系结构](../stream/ks-minidriver-architecture.md)。

2.  如果隔行扫描容器设备 GUID 存在，VMR 将启动对 [*DdMoCompCreate*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create) 回调函数的调用，以创建设备的实例。 DD MOTIONCOMPCALLBACKS 的 **CreateMoComp** 成员指向 \_ 回调函数。 在**DdMoCompCreate**调用中，指向容器设备 GUID 的指针是在[**DD \_ CREATEMOCOMPDATA**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)结构的**lpGuid**成员中指定的。 容器设备 GUID 定义如下：

    ```cpp
    DEFINE_GUID(DXVA_DeinterlaceContainerDevice, 0x0e85cb93,0x3046,0x4ff0,0xae,0xcc,0xd5,0x8c,0xb5,0xf0,0x35,0xfd);
    ```

3.  若要确定 ProcAmp 控制设备的功能，VMR 启动对驱动程序提供的 [*DdMoCompRender*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数的调用。 DD MOTIONCOMPCALLBACKS 的 **RenderMoComp** 成员指向 \_ 回调函数。 在**DdMoCompRender**调用中， *DXVA*) 中定义的**DXVA \_ ProcAmpControlQueryCapsFnCode**常量 (在[**DD \_ dwFunction**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构的**RENDERMOCOMPDATA**成员中进行了设置。 DD RENDERMOCOMPDATA 的 **lpInputData** 成员 \_ 通过指向 [**DXVA \_ VideoDesc**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc) 结构将输入参数传递给驱动程序。 驱动程序通过 DD RENDERMOCOMPDATA 的 **lpOutputData** 成员返回其输出 \_ ; **lpOutputData** 指向 [**DXVA \_ ProcAmpControlCaps**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps) 结构。

    如果驱动程序实现了 [**ProcAmpControlQueryCaps**](./dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps.md) 示例函数， [*DdMoCompRender*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数将调用 **ProcAmpControlQueryCaps**。

4.  对于硬件支持的每个 ProcAmp 调整属性，VMR 启动对驱动程序提供的 **DdMoCompRender**回调函数的调用。 在**DdMoCompRender**调用中， *DXVA*) 中定义的**DXVA \_ ProcAmpControlQueryCapsFnCode**常量 (在 DD dwFunction 的**RENDERMOCOMPDATA**成员中进行了设置 \_ 。 DD RENDERMOCOMPDATA 的 **lpInputData** 成员 \_ 通过指向已完成的 [**DXVA \_ ProcAmpControlQueryRange**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolqueryrange) 结构将输入参数传递给驱动程序。 驱动程序通过 DD RENDERMOCOMPDATA 的 **lpOutputData** 成员返回其输出 \_ ; **lpOutputData** 指向 [**DXVA \_ VideoPropertyRange**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videopropertyrange) 结构。

    如果驱动程序实现了 [**ProcAmpControlQueryRange**](./dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange.md) 示例函数， [*DdMoCompRender*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数将调用 **ProcAmpControlQueryRange**。

5.  VMR 确定硬件的 ProcAmp 调整能力后，会启动对 [*DdMoCompCreate*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create) 的调用，以创建 ProcAmp 控制设备的实例。 在 *DdMoCompCreate* 调用中，指向 ProcAmp 控制设备 GUID 的指针是在 DD CREATEMOCOMPDATA 的 **lpGuid** 成员中指定的 \_ 。 ProcAmp 控件设备 GUID 定义如下：

    ```cpp
    DEFINE_GUID(DXVA_ProcAmpControlDevice, 0x9f200913,0x2ffd,0x4056,0x9f,0x1e,0xe1,0xb5,0x08,0xf2,0x2d,0xcf); 
    ```

    如果驱动程序实现了 [**ProcAmpControlOpenStream**](./dxva-procampcontroldeviceclass-procampcontrolopenstream.md) 示例函数， [*DdMoCompCreate*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create) 回调函数将调用 **ProcAmpControlOpenStream**。

6.  对于每个 ProcAmp 调整操作，VMR 将启动对驱动程序提供的 **DdMoCompRender**回调函数的调用。 在**DdMoCompRender**调用中， *DXVA*) 中定义的**DXVA \_ ProcAmpControlQueryCapsFnCode**常量 (在[**DD \_ dwFunction**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)的**RENDERMOCOMPDATA**成员中进行了设置。 DD RENDERMOCOMPDATA 的 **lpBufferInfo** 成员指向 \_ 描述目标和源表面的两个缓冲区的数组。 DD RENDERMOCOMPDATA 的 **lpInputData** 成员 \_ 通过指向已完成的 [**DXVA \_ ProcAmpControlBlt**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolblt) 结构将输入参数传递给驱动程序。 驱动程序未返回任何输出;也就是说，DD RENDERMOCOMPDATA 的 **lpOutputData** 成员 \_ 为 **NULL**。

    如果驱动程序实现了 [**ProcAmpControlBlt**](./dxva-procampcontroldeviceclass-procampcontrolblt.md) 示例函数， **DdMoCompRender** 回调函数将调用 **ProcAmpControlBlt**。

7.  当 VMR 不再需要执行更多的 ProcAmp 控制操作时，将调用驱动程序提供的 [*DdMoCompDestroy*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy) 回调函数。 DD MOTIONCOMPCALLBACKS 的 **DestroyMoComp** 成员指向 \_ 回调函数。

    如果驱动程序实现了 [**ProcAmpControlCloseStream**](./dxva-procampcontroldeviceclass-procampcontrolclosestream.md) 示例函数， **DdMoCompDestroy** 回调函数将调用 **ProcAmpControlCloseStream**。

8.  驱动程序释放 ProcAmp 控制设备使用的所有资源。

 

