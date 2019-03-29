---
title: 从用户模式组件调用 COPP DDI
description: 从用户模式组件调用 COPP DDI
ms.assetid: f7ce10d3-bf52-4bfd-9ae8-63213a59d1c9
keywords:
- 调用 COPP DDI WDK DirectX VA
- 用户模式组件都会调用 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d7a054180da99e52402cc6958918973569dac0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563921"
---
# <a name="calling-the-copp-ddi-from-a-user-mode-component"></a>从用户模式组件调用 COPP DDI


## <span id="ddk_calling_the_copp_ddi_from_a_user_mode_component_gg"></span><span id="DDK_CALLING_THE_COPP_DDI_FROM_A_USER_MODE_COMPONENT_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

用户模式组件，如 VMR，启动对 COPP DDI 的调用。

显示驱动程序，以便 VMR 可以通知微型端口驱动程序，以将保护应用到图形适配器的视频输出，必须实现[动作补偿回调函数](motion-compensation-callbacks.md)，通过将成员所定义[**DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)结构。

若要简化驱动程序开发，驱动程序编写人员可以使用一个运动补偿代码模板，实现 COPP Ioctl 并[COPP 示例函数](sample-functions-for-copp.md)。 显示驱动程序和视频的微型端口驱动程序使用 COPP Ioctl 进行通信。 有关详细信息，请参阅[从显示器驱动程序调用 COPP DDI](calling-the-copp-ddi-from-the-display-driver.md)。 运动补偿代码模板启动对 COPP 示例函数的调用。 有关使用运动补偿代码模板的详细信息，请参阅[DirectX VA 设备的示例代码](example-code-for-directx-va-devices.md)。

以下步骤说明如何 VMR 启动对 COPP DDI 的调用：

1.  VMR 添加到筛选器关系图，它启动对显示驱动程序所提供的调用[ *DdMoCompGetGuids* ](https://msdn.microsoft.com/library/windows/hardware/ff550236)回调函数来检索驱动程序支持的设备的列表。 **GetMoCompGuids** DD 成员\_MOTIONCOMPCALLBACKS 结构，此回调函数的点。 有关筛选器关系图的详细信息，请参阅[KS 微型驱动程序体系结构](https://msdn.microsoft.com/library/windows/hardware/ff567656)。

2.  如果 DirectX VA COPP 设备 GUID 已存在，则启动对调用时 VMR [ *DdMoCompCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff549656)回调函数来初始化 COPP 设备上当前的视频会话。 **CreateMoComp** DD 成员\_MOTIONCOMPCALLBACKS 指向回调函数。 在中*DdMoCompCreate*调用中指定 GUID 的 COPP 设备的指针**lpGuid**的成员[ **DD\_CREATEMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff550529)结构。 COPP 设备 GUID 定义，如下所示：

    ```cpp
    DEFINE_GUID(DXVA_COPPDevice, 0xd2457add,0x8999,0x45ed,0x8a,0x8a,0xd1,0xaa,0x04,0x7b,0xa4,0xd5);
    ```

    显示驱动程序必须使用 COPP IOCTL 通信使用微型端口驱动程序。 如果视频的微型端口驱动程序实现[ *COPPOpenVideoSession* ](https://msdn.microsoft.com/library/windows/hardware/ff539650)示例函数，则[ *DdMoCompCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff549656)回调函数会初始化到调用**COPPOpenVideoSession**。

3.  若要确定应应用于当前的视频会话的长度可变的图形硬件证书的长度，VMR 启动对显示驱动程序所提供的调用[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)回调函数。 **RenderMoComp**的成员[ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)指向回调函数。 在中**DdMoCompRender**调用，请**dwFunction**的成员[ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)设置为值**DXVA\_COPPGetCertificateLengthFnCode** (在中定义*dxva.h*)。 显示驱动程序不会收到此调用; 中的任何输入即**lpInputData** DD 成员\_RENDERMOCOMPDATA 是**NULL**。 显示驱动程序返回的证书通过长度**lpOutputData** DD 成员\_RENDERMOCOMPDATA;**lpOutputData**指向 DWORD 数据类型。

    显示驱动程序必须使用 COPP IOCTL 通信使用微型端口驱动程序。 如果视频的微型端口驱动程序实现[ *COPPGetCertificateLength* ](https://msdn.microsoft.com/library/windows/hardware/ff539644)示例函数，则**DdMoCompRender**启动对调用时的回调函数*COPPGetCertificateLength*。

4.  若要检索的图形硬件使用的证书，VMR 启动对显示驱动程序所提供的调用**DdMoCompRender**回调函数。 在中**DdMoCompRender**调用，请**dwFunction** DD 成员\_RENDERMOCOMPDATA 设置为值**DXVA\_COPPKeyExchangeFnCode** (在中定义*dxva.h*)。 显示驱动程序不会收到此调用; 中的任何输入即**lpInputData** DD 成员\_RENDERMOCOMPDATA 是**NULL**。 **LpBufferInfo** DD 成员\_RENDERMOCOMPDATA 指向一个 RGB32 系统内存图面，其中包含要存储证书的显示驱动程序所需的空间。 显示驱动程序将返回它通过生成的 128 位随机数字**lpOutputData** DD 成员\_RENDERMOCOMPDATA。

    显示驱动程序必须使用 COPP IOCTL 通信使用微型端口驱动程序。 如果视频的微型端口驱动程序实现[ *COPPKeyExchange* ](https://msdn.microsoft.com/library/windows/hardware/ff539646)示例函数，则[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)回调函数启动对调用*COPPKeyExchange*。

5.  若要将当前的视频会话设置为受保护模式，VMR 启动对显示驱动程序所提供的调用[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)回调函数。 在中*DdMoCompRender*调用，请**dwFunction** DD 成员\_RENDERMOCOMPDATA 设置为值**DXVA\_COPPSequenceStartFnCode**(在中定义*dxva.h*)。 **LpInputData** DD 成员\_RENDERMOCOMPDATA 将传递输入的命令和状态序列起始代码到显示器驱动程序通过指向已完成[ **DXVA\_COPPSignature** ](https://msdn.microsoft.com/library/windows/hardware/ff563150)结构。 显示驱动程序不返回任何输出;即**lpOutputData** DD 成员\_RENDERMOCOMPDATA 是**NULL**。

    显示驱动程序必须使用 COPP IOCTL 通信使用微型端口驱动程序。 如果视频的微型端口驱动程序实现[ *COPPSequenceStart* ](https://msdn.microsoft.com/library/windows/hardware/ff540421)示例函数，则[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)回调函数启动对调用**COPPSequenceStart**。

6.  若要在与 DirectX VA COPP 设备相关联的物理连接器上设置保护级别，VMR 启动对显示驱动程序所提供的调用[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)回调函数。 在中*DdMoCompRender*调用，请**dwFunction** DD 成员\_RENDERMOCOMPDATA 设置为值**DXVA\_COPPCommandFnCode** (在中定义*dxva.h*)。 **LpInputData** DD 成员\_RENDERMOCOMPDATA 传递输入的参数通过指向已完成显示器驱动程序[ **DXVA\_COPPCommand**](https://msdn.microsoft.com/library/windows/hardware/ff563141)结构。 显示驱动程序不返回任何输出;即**lpOutputData** DD 成员\_RENDERMOCOMPDATA 是**NULL**。

    显示驱动程序必须使用 COPP IOCTL 通信使用微型端口驱动程序。 如果视频的微型端口驱动程序实现[ *COPPCommand* ](https://msdn.microsoft.com/library/windows/hardware/ff539642)示例函数，则[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)回调函数启动对调用*COPPCommand*。

7.  若要检索有关正在使用的物理连接器保护信息，VMR 启动对显示驱动程序所提供的调用[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)回调函数。 在中*DdMoCompRender*调用，请**dwFunction** DD 成员\_RENDERMOCOMPDATA 设置为值**DXVA\_COPPQueryStatusFnCode** (在中定义*dxva.h*)。 **LpInputData** DD 成员\_RENDERMOCOMPDATA 传递输入的参数通过指向已完成显示器驱动程序[ **DXVA\_COPPStatusInput**](https://msdn.microsoft.com/library/windows/hardware/ff563899)结构。 显示驱动程序将通过其输出返回**lpOutputData** DD 成员\_RENDERMOCOMPDATA;**lpOutputData**指向[ **DXVA\_COPPStatusOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff563903)结构。

    显示驱动程序必须使用 COPP IOCTL 通信使用微型端口驱动程序。 如果视频的微型端口驱动程序实现[ *COPPQueryStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff539652)示例函数，则[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)回调函数启动对调用*COPPQueryStatus*。

8.  当不再需要执行任何更多的 COPP 操作 VMR 时，显示器驱动程序提供[ *DdMoCompDestroy* ](https://msdn.microsoft.com/library/windows/hardware/ff549664)调用回调函数。 **DestroyMoComp** DD 成员\_MOTIONCOMPCALLBACKS 指向回调函数。

    显示驱动程序必须使用 COPP IOCTL 通信使用微型端口驱动程序。 如果视频的微型端口驱动程序实现[ *COPPCloseVideoSession* ](https://msdn.microsoft.com/library/windows/hardware/ff539638)示例函数，则**DdMoCompDestroy**回调函数会初始化调用*COPPCloseVideoSession*。

9.  在驱动程序然后释放使用 DirectX VA COPP 设备的任何资源。

 

 





