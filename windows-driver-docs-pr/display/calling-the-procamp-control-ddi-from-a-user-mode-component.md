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
ms.openlocfilehash: 1a6fd20cf863b0e7bac842b1ec421b149891ee44
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385704"
---
# <a name="calling-the-procamp-control-ddi-from-a-user-mode-component"></a>从用户模式组件调用 ProcAmp 控制 DDI


## <span id="ddk_calling_the_procamp_control_ddi_from_a_user_mode_component_gg"></span><span id="DDK_CALLING_THE_PROCAMP_CONTROL_DDI_FROM_A_USER_MODE_COMPONENT_GG"></span>


用户模式组件，如 VMR，启动对调用[ProcAmp 控件 DDI](https://msdn.microsoft.com/library/windows/hardware/ff569186)。

显示驱动程序，以便 VMR 可以访问 ProcAmp 控件功能，必须实现[动作补偿回调函数](motion-compensation-callbacks.md)，其定义的成员[ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)结构。

若要简化驱动程序开发，驱动程序编写人员可以使用运动补偿代码模板，并实现[ProcAmp 控件示例函数](sample-functions-for-procamp-control.md)。 运动补偿模板调用其 ProcAmp 控件示例函数来执行 ProcAmp 控制操作。 有关使用运动补偿模板的详细信息，请参阅[DirectX VA 设备的示例代码](example-code-for-directx-va-devices.md)。

以下步骤说明如何 VMR 启动对 ProcAmp 控件 DDI 的调用：

1.  VMR 添加到筛选器关系图，它启动的驱动程序提供对的调用[ *DdMoCompGetGuids* ](https://msdn.microsoft.com/library/windows/hardware/ff550236)回调函数来检索驱动程序支持的设备的列表。 **GetMoCompGuids** DD 成员\_MOTIONCOMPCALLBACKS 指向此回调函数。 有关筛选器关系图的详细信息，请参阅[KS 微型驱动程序体系结构](https://msdn.microsoft.com/library/windows/hardware/ff567656)。

2.  如果存在取消隔行扫描容器设备 GUID，则 VMR 开始调用[ *DdMoCompCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff549656)回调函数来创建设备的实例。 **CreateMoComp** DD 成员\_MOTIONCOMPCALLBACKS 指向回调函数。 在中**DdMoCompCreate**调用中指定 GUID 的容器设备的指针**lpGuid**的成员[ **DD\_CREATEMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff550529)结构。 容器设备 GUID 定义，如下所示：

    ```cpp
    DEFINE_GUID(DXVA_DeinterlaceContainerDevice, 0x0e85cb93,0x3046,0x4ff0,0xae,0xcc,0xd5,0x8c,0xb5,0xf0,0x35,0xfd);
    ```

3.  若要确定 ProcAmp 控制设备的功能，VMR 启动对驱动程序提供的调用[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)回调函数。 **RenderMoComp** DD 成员\_MOTIONCOMPCALLBACKS 指向回调函数。 在中**DdMoCompRender**调用，请**DXVA\_ProcAmpControlQueryCapsFnCode**常量 (在中定义*dxva.h*) 中设置**dwFunction**的成员[ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)结构。 **LpInputData** DD 成员\_RENDERMOCOMPDATA 传递到驱动程序的输入的参数传递通过指向[ **DXVA\_VideoDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff564070)结构。 该驱动程序将通过其输出返回**lpOutputData** DD 成员\_RENDERMOCOMPDATA;**lpOutputData**指向[ **DXVA\_ProcAmpControlCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff564019)结构。

    如果该驱动程序实现[ **ProcAmpControlQueryCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff563949)示例函数[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)回调函数调用**ProcAmpControlQueryCaps**。

4.  对于每个硬件支持 ProcAmp 调整属性，VMR 启动的驱动程序提供对的调用**DdMoCompRender**回调函数。 在中**DdMoCompRender**调用，请**DXVA\_ProcAmpControlQueryCapsFnCode**常量 (在中定义*dxva.h*) 中设置**dwFunction** DD 成员\_RENDERMOCOMPDATA。 **LpInputData** DD 成员\_RENDERMOCOMPDATA 传递到驱动程序的输入的参数传递通过指向已完成[ **DXVA\_ProcAmpControlQueryRange**](https://msdn.microsoft.com/library/windows/hardware/ff564032)结构。 该驱动程序将通过其输出返回**lpOutputData** DD 成员\_RENDERMOCOMPDATA;**lpOutputData**指向[ **DXVA\_VideoPropertyRange** ](https://msdn.microsoft.com/library/windows/hardware/ff564083)结构。

    如果该驱动程序实现[ **ProcAmpControlQueryRange** ](https://msdn.microsoft.com/library/windows/hardware/ff563950)示例函数[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)回调函数调用**ProcAmpControlQueryRange**。

5.  VMR 已确定的硬件的 ProcAmp 调整功能后，它开始调用[ *DdMoCompCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff549656)创建 ProcAmp 控制设备的实例。 在中*DdMoCompCreate*调用中指定 GUID 的 ProcAmp 控制设备的指针**lpGuid** DD 成员\_CREATEMOCOMPDATA。 ProcAmp 控制设备 GUID 定义，如下所示：

    ```cpp
    DEFINE_GUID(DXVA_ProcAmpControlDevice, 0x9f200913,0x2ffd,0x4056,0x9f,0x1e,0xe1,0xb5,0x08,0xf2,0x2d,0xcf); 
    ```

    如果该驱动程序实现[ **ProcAmpControlOpenStream** ](https://msdn.microsoft.com/library/windows/hardware/ff564026)示例函数[ *DdMoCompCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff549656)回调函数调用**ProcAmpControlOpenStream**。

6.  对于每个 ProcAmp 调整操作，VMR 启动的驱动程序提供对的调用**DdMoCompRender**回调函数。 在中**DdMoCompRender**调用，请**DXVA\_ProcAmpControlQueryCapsFnCode**常量 (在中定义*dxva.h*) 中设置**dwFunction**的成员[ **DD\_RENDERMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551693)。 **LpBufferInfo** DD 成员\_RENDERMOCOMPDATA 指向描述目标和源曲面的两个缓冲区的数组。 **LpInputData** DD 成员\_RENDERMOCOMPDATA 传递到驱动程序的输入的参数传递通过指向已完成[ **DXVA\_ProcAmpControlBlt**](https://msdn.microsoft.com/library/windows/hardware/ff564015)结构。 该驱动程序不返回任何输出;即**lpOutputData** DD 成员\_RENDERMOCOMPDATA 是**NULL**。

    如果该驱动程序实现[ **ProcAmpControlBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff564022)示例函数**DdMoCompRender**回调函数调用**ProcAmpControlBlt**.

7.  当 VMR 不再需要执行其他任何 ProcAmp 管理操作，驱动程序提供[ *DdMoCompDestroy* ](https://msdn.microsoft.com/library/windows/hardware/ff549664)调用回调函数。 **DestroyMoComp** DD 成员\_MOTIONCOMPCALLBACKS 指向回调函数。

    如果该驱动程序实现[ **ProcAmpControlCloseStream** ](https://msdn.microsoft.com/library/windows/hardware/ff564025)示例函数**DdMoCompDestroy**回调函数调用**ProcAmpControlCloseStream**。

8.  该驱动程序释放 ProcAmp 控制设备使用的所有资源。

 

 





