---
title: 从用户模式组件调用 COPP DDI
description: 从用户模式组件调用 COPP DDI
ms.assetid: f7ce10d3-bf52-4bfd-9ae8-63213a59d1c9
keywords:
- 调用 COPP DDI WDK DirectX VA
- 用户模式组件都会调用 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09dfbd3182bcf901337f2d82a442bd5f3745d4ba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384604"
---
# <a name="calling-the-copp-ddi-from-a-user-mode-component"></a>从用户模式组件调用 COPP DDI


## <span id="ddk_calling_the_copp_ddi_from_a_user_mode_component_gg"></span><span id="DDK_CALLING_THE_COPP_DDI_FROM_A_USER_MODE_COMPONENT_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

用户模式组件，如 VMR，启动对 COPP DDI 的调用。

显示驱动程序，以便 VMR 可以通知微型端口驱动程序，以将保护应用到图形适配器的视频输出，必须实现[动作补偿回调函数](motion-compensation-callbacks.md)，通过将成员所定义[**DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构。

若要简化驱动程序开发，驱动程序编写人员可以使用一个运动补偿代码模板，实现 COPP Ioctl 并[COPP 示例函数](sample-functions-for-copp.md)。 显示驱动程序和视频的微型端口驱动程序使用 COPP Ioctl 进行通信。 有关详细信息，请参阅[从显示器驱动程序调用 COPP DDI](calling-the-copp-ddi-from-the-display-driver.md)。 运动补偿代码模板启动对 COPP 示例函数的调用。 有关使用运动补偿代码模板的详细信息，请参阅[DirectX VA 设备的示例代码](example-code-for-directx-va-devices.md)。

以下步骤说明如何 VMR 启动对 COPP DDI 的调用：

1.  VMR 添加到筛选器关系图，它启动对显示驱动程序所提供的调用[ *DdMoCompGetGuids* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)回调函数来检索驱动程序支持的设备的列表。 **GetMoCompGuids** DD 成员\_MOTIONCOMPCALLBACKS 结构，此回调函数的点。 有关筛选器关系图的详细信息，请参阅[KS 微型驱动程序体系结构](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-minidriver-architecture)。

2.  如果 DirectX VA COPP 设备 GUID 已存在，则启动对调用时 VMR [ *DdMoCompCreate* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)回调函数来初始化 COPP 设备上当前的视频会话。 **CreateMoComp** DD 成员\_MOTIONCOMPCALLBACKS 指向回调函数。 在中*DdMoCompCreate*调用中指定 GUID 的 COPP 设备的指针**lpGuid**的成员[ **DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)结构。 COPP 设备 GUID 定义，如下所示：

    ```cpp
    DEFINE_GUID(DXVA_COPPDevice, 0xd2457add,0x8999,0x45ed,0x8a,0x8a,0xd1,0xaa,0x04,0x7b,0xa4,0xd5);
    ```

    显示驱动程序必须使用 COPP IOCTL 通信使用微型端口驱动程序。 如果视频的微型端口驱动程序实现[ *COPPOpenVideoSession* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppopenvideosession)示例函数，则[ *DdMoCompCreate* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)回调函数会初始化到调用**COPPOpenVideoSession**。

3.  若要确定应应用于当前的视频会话的长度可变的图形硬件证书的长度，VMR 启动对显示驱动程序所提供的调用[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数。 **RenderMoComp**的成员[ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)指向回调函数。 在中**DdMoCompRender**调用，请**dwFunction**的成员[ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)设置为值**DXVA\_COPPGetCertificateLengthFnCode** (在中定义*dxva.h*)。 显示驱动程序不会收到此调用; 中的任何输入即**lpInputData** DD 成员\_RENDERMOCOMPDATA 是**NULL**。 显示驱动程序返回的证书通过长度**lpOutputData** DD 成员\_RENDERMOCOMPDATA;**lpOutputData**指向 DWORD 数据类型。

    显示驱动程序必须使用 COPP IOCTL 通信使用微型端口驱动程序。 如果视频的微型端口驱动程序实现[ *COPPGetCertificateLength* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppgetcertificatelength)示例函数，则**DdMoCompRender**启动对调用时的回调函数*COPPGetCertificateLength*。

4.  若要检索的图形硬件使用的证书，VMR 启动对显示驱动程序所提供的调用**DdMoCompRender**回调函数。 在中**DdMoCompRender**调用，请**dwFunction** DD 成员\_RENDERMOCOMPDATA 设置为值**DXVA\_COPPKeyExchangeFnCode** (在中定义*dxva.h*)。 显示驱动程序不会收到此调用; 中的任何输入即**lpInputData** DD 成员\_RENDERMOCOMPDATA 是**NULL**。 **LpBufferInfo** DD 成员\_RENDERMOCOMPDATA 指向一个 RGB32 系统内存图面，其中包含要存储证书的显示驱动程序所需的空间。 显示驱动程序将返回它通过生成的 128 位随机数字**lpOutputData** DD 成员\_RENDERMOCOMPDATA。

    显示驱动程序必须使用 COPP IOCTL 通信使用微型端口驱动程序。 如果视频的微型端口驱动程序实现[ *COPPKeyExchange* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppkeyexchange)示例函数，则[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数启动对调用*COPPKeyExchange*。

5.  若要将当前的视频会话设置为受保护模式，VMR 启动对显示驱动程序所提供的调用[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数。 在中*DdMoCompRender*调用，请**dwFunction** DD 成员\_RENDERMOCOMPDATA 设置为值**DXVA\_COPPSequenceStartFnCode**(在中定义*dxva.h*)。 **LpInputData** DD 成员\_RENDERMOCOMPDATA 将传递输入的命令和状态序列起始代码到显示器驱动程序通过指向已完成[ **DXVA\_COPPSignature** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppsignature)结构。 显示驱动程序不返回任何输出;即**lpOutputData** DD 成员\_RENDERMOCOMPDATA 是**NULL**。

    显示驱动程序必须使用 COPP IOCTL 通信使用微型端口驱动程序。 如果视频的微型端口驱动程序实现[ *COPPSequenceStart* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppsequencestart)示例函数，则[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数启动对调用**COPPSequenceStart**。

6.  若要在与 DirectX VA COPP 设备相关联的物理连接器上设置保护级别，VMR 启动对显示驱动程序所提供的调用[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数。 在中*DdMoCompRender*调用，请**dwFunction** DD 成员\_RENDERMOCOMPDATA 设置为值**DXVA\_COPPCommandFnCode** (在中定义*dxva.h*)。 **LpInputData** DD 成员\_RENDERMOCOMPDATA 传递输入的参数通过指向已完成显示器驱动程序[ **DXVA\_COPPCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppcommand)结构。 显示驱动程序不返回任何输出;即**lpOutputData** DD 成员\_RENDERMOCOMPDATA 是**NULL**。

    显示驱动程序必须使用 COPP IOCTL 通信使用微型端口驱动程序。 如果视频的微型端口驱动程序实现[ *COPPCommand* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)示例函数，则[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数启动对调用*COPPCommand*。

7.  若要检索有关正在使用的物理连接器保护信息，VMR 启动对显示驱动程序所提供的调用[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数。 在中*DdMoCompRender*调用，请**dwFunction** DD 成员\_RENDERMOCOMPDATA 设置为值**DXVA\_COPPQueryStatusFnCode** (在中定义*dxva.h*)。 **LpInputData** DD 成员\_RENDERMOCOMPDATA 传递输入的参数通过指向已完成显示器驱动程序[ **DXVA\_COPPStatusInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppstatusinput)结构。 显示驱动程序将通过其输出返回**lpOutputData** DD 成员\_RENDERMOCOMPDATA;**lpOutputData**指向[ **DXVA\_COPPStatusOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppstatusoutput)结构。

    显示驱动程序必须使用 COPP IOCTL 通信使用微型端口驱动程序。 如果视频的微型端口驱动程序实现[ *COPPQueryStatus* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)示例函数，则[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数启动对调用*COPPQueryStatus*。

8.  当不再需要执行任何更多的 COPP 操作 VMR 时，显示器驱动程序提供[ *DdMoCompDestroy* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)调用回调函数。 **DestroyMoComp** DD 成员\_MOTIONCOMPCALLBACKS 指向回调函数。

    显示驱动程序必须使用 COPP IOCTL 通信使用微型端口驱动程序。 如果视频的微型端口驱动程序实现[ *COPPCloseVideoSession* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppclosevideosession)示例函数，则**DdMoCompDestroy**回调函数会初始化调用*COPPCloseVideoSession*。

9.  在驱动程序然后释放使用 DirectX VA COPP 设备的任何资源。

 

 





