---
title: 从用户模式组件调用反交错 DDI
description: 从用户模式组件调用反交错 DDI
ms.assetid: 3ec18c7e-02dc-4607-b280-3ca1bc5d2839
keywords:
- 调用取消隔行扫描 DDI WDK DirectX VA
- 用户模式组件都会调用 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a947b3a84bea842a68d57e1a5c581067cc7dbc1f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384601"
---
# <a name="calling-the-deinterlace-ddi-from-a-user-mode-component"></a>从用户模式组件调用反交错 DDI


## <span id="ddk_calling_the_deinterlace_ddi_from_a_user_mode_component_gg"></span><span id="DDK_CALLING_THE_DEINTERLACE_DDI_FROM_A_USER_MODE_COMPONENT_GG"></span>


用户模式组件，如 VMR，启动对取消隔行扫描 DDI 的调用。

显示驱动程序，以便 VMR 可以取消隔行扫描，并对视频内容执行帧速率转换，必须实现[动作补偿回调函数](motion-compensation-callbacks.md)，其定义的成员[ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构。

若要简化驱动程序开发，驱动程序编写人员可以使用一个运动补偿代码模板并实现[去隔行示例函数](sample-functions-for-deinterlacing.md)。 运动补偿模板调用取消隔行扫描的示例函数，来对视频内容执行取消隔行和帧速率转换。 有关使用运动补偿模板的详细信息，请参阅[DirectX VA 设备的示例代码](example-code-for-directx-va-devices.md)。

以下步骤说明如何 VMR 启动对取消隔行扫描 DDI 的调用：

1.  VMR 添加到筛选器关系图，它启动的驱动程序提供对的调用[ *DdMoCompGetGuids* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)回调函数来检索驱动程序支持的设备的列表。 **GetMoCompGuids** DD 成员\_MOTIONCOMPCALLBACKS 结构，此回调函数的点。 有关筛选器关系图的详细信息，请参阅[KS 微型驱动程序体系结构](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-minidriver-architecture)。

2.  如果存在取消隔行扫描容器设备 GUID，则 VMR 开始调用[ *DdMoCompCreate* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)回调函数来创建设备的实例。 **CreateMoComp** DD 成员\_MOTIONCOMPCALLBACKS 指向回调函数。 在中*DdMoCompCreate*调用中指定 GUID 的容器设备的指针**lpGuid**的成员[ **DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)结构。 容器设备 GUID 定义，如下所示：
    ```cpp
    DEFINE_GUID(DXVA_DeinterlaceContainerDevice, 0x0e85cb93,0x3046,0x4ff0,0xae,0xcc,0xd5,0x8c,0xb5,0xf0,0x35,0xfd);
    ```

3.  若要确定特定的输入视频格式的可用去隔行或帧速率转换模式，VMR 启动对驱动程序提供的调用[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数。 **RenderMoComp**的成员[ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)指向回调函数。 在中**DdMoCompRender**调用，请**DXVA\_ProcAmpControlQueryCapsFnCode**常量 (在中定义*dxva.h*) 中设置**dwFunction**的成员[ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构。 **LpInputData** DD 成员\_RENDERMOCOMPDATA 传递到驱动程序的输入的参数传递通过指向已完成[ **DXVA\_VideoDesc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)结构。 该驱动程序将通过其输出返回**lpOutputData** DD 成员\_RENDERMOCOMPDATA;**lpOutputData**指向[ **DXVA\_DeinterlaceQueryAvailableModes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacequeryavailablemodes)结构。

    如果该驱动程序实现[ **DeinterlaceQueryAvailableModes** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes)示例函数**DdMoCompRender**回调函数调用**DeinterlaceQueryAvailableModes**。

4.  对于每个取消隔行扫描模式驱动程序支持，VMR 启动对驱动程序提供的调用**DdMoCompRender**回调函数。 在中**DdMoCompRender**调用，请**DXVA\_DeinterlaceQueryModeCapsFnCode**常量 (在中定义*dxva.h*) 中设置**dwFunction** DD 成员\_RENDERMOCOMPDATA。 **LpInputData** DD 成员\_RENDERMOCOMPDATA 传递到驱动程序的输入的参数传递通过指向已完成[ **DXVA\_DeinterlaceQueryModeCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacequerymodecaps)结构。 该驱动程序将通过其输出返回**lpOutputData** DD 成员\_RENDERMOCOMPDATA;**lpOutputData**指向[ **DXVA\_DeinterlaceCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)结构。

    如果该驱动程序实现[ **DeinterlaceQueryModeCaps** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)示例函数**DdMoCompRender**回调函数调用**DeinterlaceQueryModeCaps**。

5.  VMR 已确定去隔行后的特定功能取消隔行扫描模式 (例如，bob 去隔行)，它开始调用[ *DdMoCompCreate* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)若要创建的实例取消隔行扫描模式设备 （例如，取消隔行扫描 bob 设备）。 在中*DdMoCompCreate*调用中指定 GUID 的取消隔行扫描模式设备的指针**lpGuid** DD 成员\_CREATEMOCOMPDATA。 取消隔行扫描 bob 设备 GUID 定义，如下所示：

    ```cpp
    DEFINE_GUID(DXVAp_DeinterlaceBobDevice, 0x335aa36e,0x7884,0x43a4,0x9c,0x91,0x7f,0x87,0xfa,0xf3,0xe3,0x7e);
    ```

    如果该驱动程序实现[ **DeinterlaceOpenStream** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceopenstream)示例函数[ *DdMoCompCreate* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)回调函数调用**DeinterlaceOpenStream**。

6.  对于每个取消隔行扫描操作，启动到的驱动程序提供的调用时 VMR [ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数。 在中*DdMoCompRender*调用，请**DXVA\_ProcAmpControlQueryCapsFnCode**常量 (在中定义*dxva.h*) 中设置**dwFunction** DD 成员\_RENDERMOCOMPDATA。 **LpBufferInfo** DD 成员\_RENDERMOCOMPDATA 指向描述目标面和每个输入视频源示例的缓冲区的数组。 **LpInputData** DD 成员\_RENDERMOCOMPDATA 传递到驱动程序的输入的参数传递通过指向已完成[ **DXVA\_DeinterlaceBlt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlaceblt)结构。 该驱动程序不返回任何输出;即**lpOutputData** DD 成员\_RENDERMOCOMPDATA 是**NULL**。

    如果该驱动程序实现[ **DeinterlaceBlt** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt)示例函数**DdMoCompRender**回调函数调用**DeinterlaceBlt**。

7.  对于每个组合去隔行和子流组合的情况下操作，VMR Microsoft Windows Server 2003 SP1 及更高版本和 Windows XP SP2 和更高版本启动的驱动程序提供对的调用[ *DdMoCompRender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数。 在中*DdMoCompRender*调用，请**DXVA\_DeinterlaceBltExFnCode**常量 (在中定义*dxva.h*) 中设置**dwFunction** DD 成员\_RENDERMOCOMPDATA。 **LpBufferInfo** DD 成员\_RENDERMOCOMPDATA 指向描述目标面和每个输入视频源示例的面的缓冲区的数组。 **LpInputData** DD 成员\_RENDERMOCOMPDATA 传递到驱动程序的输入的参数传递通过指向已完成[ **DXVA\_DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacebltex)结构。 该驱动程序不返回任何输出;即**lpOutputData** DD 成员\_RENDERMOCOMPDATA 是**NULL**。

    如果该驱动程序实现[ **DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)示例函数**DdMoCompRender**回调函数调用**DeinterlaceBltEx**.

8.  当 VMR 不再需要执行任何更多取消隔行扫描操作，驱动程序提供[ *DdMoCompDestroy* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)调用回调函数。 **DestroyMoComp** DD 成员\_MOTIONCOMPCALLBACKS 指向回调函数。

    如果该驱动程序实现[ **DeinterlaceCloseStream** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceclosestream)示例函数[ *DdMoCompDestroy* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)回调函数调用**DeinterlaceCloseStream**。

9.  该驱动程序然后释放取消隔行扫描模式设备使用的所有资源。

 

 





