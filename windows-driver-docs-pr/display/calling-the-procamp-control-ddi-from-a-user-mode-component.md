---
title: 从用户模式组件调用 ProcAmp 控制 DDI
description: 从用户模式组件调用 ProcAmp 控制 DDI
ms.assetid: 1e4e19bb-eb4b-4db6-8947-429a1a414e4a
keywords:
- 调用 ProcAmp 控件 DDI WDK DirectX VA
- 用户模式组件都会调用 WDK DirectX VA
- ProcAmp WDK DirectX VA，从用户模式组件调用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fce8f52fe26f7588bc17295944dae044222feffb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384600"
---
# <a name="calling-the-procamp-control-ddi-from-a-user-mode-component"></a>从用户模式组件调用 ProcAmp 控制 DDI


## <span id="ddk_calling_the_procamp_control_ddi_from_a_user_mode_component_gg"></span><span id="DDK_CALLING_THE_PROCAMP_CONTROL_DDI_FROM_A_USER_MODE_COMPONENT_GG"></span>


用户模式组件，如 VMR，启动对调用[ProcAmp 控件 DDI](https://docs.microsoft.com/windows-hardware/drivers/display/procamp-control-ddi)。

显示驱动程序，以便 VMR 可以访问 ProcAmp 控件功能，必须实现[动作补偿回调函数](motion-compensation-callbacks.md)，其定义的成员[ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构。

若要简化驱动程序开发，驱动程序编写人员可以使用运动补偿代码模板，并实现[ProcAmp 控件示例函数](sample-functions-for-procamp-control.md)。 运动补偿模板调用其 ProcAmp 控件示例函数来执行 ProcAmp 控制操作。 有关使用运动补偿模板的详细信息，请参阅[DirectX VA 设备的示例代码](example-code-for-directx-va-devices.md)。

以下步骤说明如何 VMR 启动对 ProcAmp 控件 DDI 的调用：

1.  VMR 添加到筛选器关系图，它启动的驱动程序提供对的调用[ *DdMoCompGetGuids* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)回调函数来检索驱动程序支持的设备的列表。 **GetMoCompGuids** DD 成员\_MOTIONCOMPCALLBACKS 指向此回调函数。 有关筛选器关系图的详细信息，请参阅[KS 微型驱动程序体系结构](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-minidriver-architecture)。

2.  如果存在取消隔行扫描容器设备 GUID，则 VMR 开始调用[ *DdMoCompCreate* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)回调函数来创建设备的实例。 **CreateMoComp** DD 成员\_MOTIONCOMPCALLBACKS 指向回调函数。 在中**DdMoCompCreate**调用中指定 GUID 的容器设备的指针**lpGuid**的成员[ **DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)结构。 容器设备 GUID 定义，如下所示：

    ```cpp
    DEFINE_GUID(DXVA_DeinterlaceContainerDevice, 0x0e85cb93,0x3046,0x4ff0,0xae,0xcc,0xd5,0x8c,0xb5,0xf0,0x35,0xfd);
    ```

3.  若要确定 ProcAmp 控制设备的功能，VMR 启动对驱动程序提供的调用[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数。 **RenderMoComp** DD 成员\_MOTIONCOMPCALLBACKS 指向回调函数。 在中**DdMoCompRender**调用，请**DXVA\_ProcAmpControlQueryCapsFnCode**常量 (在中定义*dxva.h*) 中设置**dwFunction**的成员[ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构。 **LpInputData** DD 成员\_RENDERMOCOMPDATA 传递到驱动程序的输入的参数传递通过指向[ **DXVA\_VideoDesc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)结构。 该驱动程序将通过其输出返回**lpOutputData** DD 成员\_RENDERMOCOMPDATA;**lpOutputData**指向[ **DXVA\_ProcAmpControlCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_procampcontrolcaps)结构。

    如果该驱动程序实现[ **ProcAmpControlQueryCaps** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps)示例函数[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数调用**ProcAmpControlQueryCaps**。

4.  对于每个硬件支持 ProcAmp 调整属性，VMR 启动的驱动程序提供对的调用**DdMoCompRender**回调函数。 在中**DdMoCompRender**调用，请**DXVA\_ProcAmpControlQueryCapsFnCode**常量 (在中定义*dxva.h*) 中设置**dwFunction** DD 成员\_RENDERMOCOMPDATA。 **LpInputData** DD 成员\_RENDERMOCOMPDATA 传递到驱动程序的输入的参数传递通过指向已完成[ **DXVA\_ProcAmpControlQueryRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_procampcontrolqueryrange)结构。 该驱动程序将通过其输出返回**lpOutputData** DD 成员\_RENDERMOCOMPDATA;**lpOutputData**指向[ **DXVA\_VideoPropertyRange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videopropertyrange)结构。

    如果该驱动程序实现[ **ProcAmpControlQueryRange** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange)示例函数[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数调用**ProcAmpControlQueryRange**。

5.  VMR 已确定的硬件的 ProcAmp 调整功能后，它开始调用[ *DdMoCompCreate* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)创建 ProcAmp 控制设备的实例。 在中*DdMoCompCreate*调用中指定 GUID 的 ProcAmp 控制设备的指针**lpGuid** DD 成员\_CREATEMOCOMPDATA。 ProcAmp 控制设备 GUID 定义，如下所示：

    ```cpp
    DEFINE_GUID(DXVA_ProcAmpControlDevice, 0x9f200913,0x2ffd,0x4056,0x9f,0x1e,0xe1,0xb5,0x08,0xf2,0x2d,0xcf); 
    ```

    如果该驱动程序实现[ **ProcAmpControlOpenStream** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolopenstream)示例函数[ *DdMoCompCreate* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)回调函数调用**ProcAmpControlOpenStream**。

6.  对于每个 ProcAmp 调整操作，VMR 启动的驱动程序提供对的调用**DdMoCompRender**回调函数。 在中**DdMoCompRender**调用，请**DXVA\_ProcAmpControlQueryCapsFnCode**常量 (在中定义*dxva.h*) 中设置**dwFunction**的成员[ **DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)。 **LpBufferInfo** DD 成员\_RENDERMOCOMPDATA 指向描述目标和源曲面的两个缓冲区的数组。 **LpInputData** DD 成员\_RENDERMOCOMPDATA 传递到驱动程序的输入的参数传递通过指向已完成[ **DXVA\_ProcAmpControlBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_procampcontrolblt)结构。 该驱动程序不返回任何输出;即**lpOutputData** DD 成员\_RENDERMOCOMPDATA 是**NULL**。

    如果该驱动程序实现[ **ProcAmpControlBlt** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolblt)示例函数**DdMoCompRender**回调函数调用**ProcAmpControlBlt**.

7.  当 VMR 不再需要执行其他任何 ProcAmp 管理操作，驱动程序提供[ *DdMoCompDestroy* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)调用回调函数。 **DestroyMoComp** DD 成员\_MOTIONCOMPCALLBACKS 指向回调函数。

    如果该驱动程序实现[ **ProcAmpControlCloseStream** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolclosestream)示例函数**DdMoCompDestroy**回调函数调用**ProcAmpControlCloseStream**。

8.  该驱动程序释放 ProcAmp 控制设备使用的所有资源。

 

 





