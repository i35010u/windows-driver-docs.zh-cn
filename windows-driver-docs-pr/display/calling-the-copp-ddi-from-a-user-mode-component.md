---
title: 从用户模式组件调用 COPP DDI
description: 从用户模式组件调用 COPP DDI
ms.assetid: f7ce10d3-bf52-4bfd-9ae8-63213a59d1c9
keywords:
- 调用 COPP DDI WDK DirectX VA
- 用户模式组件调用 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ab4a2ce9785ef83c8f67280a9a7561e7dd27e4b
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715702"
---
# <a name="calling-the-copp-ddi-from-a-user-mode-component"></a>从用户模式组件调用 COPP DDI


## <span id="ddk_calling_the_copp_ddi_from_a_user_mode_component_gg"></span><span id="DDK_CALLING_THE_COPP_DDI_FROM_A_USER_MODE_COMPONENT_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

用户模式组件（如 VMR）启动对 COPP DDI 的调用。

为了使 VMR 能够通知视频微型端口驱动程序对图形适配器的视频输出应用保护，显示驱动程序必须实现 [运动补偿回叫函数](motion-compensation-callbacks.md)，这些函数由 [**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks) 结构的成员定义。

为了简化驱动程序开发，驱动程序编写器可以使用运动补偿代码模板，并实现 COPP IOCTLs 和 [COPP 示例函数](sample-functions-for-copp.md)。 显示驱动程序和视频微型端口驱动程序使用 COPP IOCTLs 进行通信。 有关详细信息，请参阅 [从显示驱动程序调用 COPP DDI](calling-the-copp-ddi-from-the-display-driver.md)。 运动补偿代码模板启动对 COPP 示例函数的调用。 有关使用运动补偿代码模板的详细信息，请参阅 [DIRECTX VA 设备的示例代码](example-code-for-directx-va-devices.md)。

以下步骤说明了 VMR 如何发起对 COPP DDI 的调用：

1.  将 VMR 添加到筛选器图时，它将启动对显示驱动程序提供的 [*DdMoCompGetGuids*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids) 回调函数的调用，以检索该驱动程序支持的设备的列表。 DD MOTIONCOMPCALLBACKS 结构的 **GetMoCompGuids** 成员 \_ 指向此回调函数。 有关筛选器关系图的详细信息，请参阅 [KS 微型驱动程序体系结构](../stream/ks-minidriver-architecture.md)。

2.  如果 DirectX VA COPP 设备 GUID 存在，则 VMR 将启动对 [*DdMoCompCreate*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_create) 回调函数的调用，以在当前视频会话上初始化 COPP 设备。 DD MOTIONCOMPCALLBACKS 的 **CreateMoComp** 成员指向 \_ 回调函数。 在*DdMoCompCreate*调用中，指向 COPP 设备 GUID 的指针是在[**DD \_ CREATEMOCOMPDATA**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_createmocompdata)结构的**lpGuid**成员中指定的。 COPP 设备 GUID 定义如下：

    ```cpp
    DEFINE_GUID(DXVA_COPPDevice, 0xd2457add,0x8999,0x45ed,0x8a,0x8a,0xd1,0xaa,0x04,0x7b,0xa4,0xd5);
    ```

    显示驱动程序必须使用 COPP IOCTL 与视频微型端口驱动程序通信。 如果视频微型端口驱动程序实现了 [*COPPOpenVideoSession*](./coppopenvideosession.md) 示例函数，则 [*DdMoCompCreate*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_create) 回调函数将启动对 **COPPOpenVideoSession**的调用。

3.  若要确定应对当前视频会话使用的可变长度图形硬件证书的长度，VMR 将启动对显示驱动程序提供的 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数的调用。 [**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)的**RenderMoComp**成员指向回调函数。 在**DdMoCompRender**调用中， [**DD \_ RENDERMOCOMPDATA**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)的**dwFunction**成员设置为*COPPGetCertificateLengthFnCode*) 中定义的**DXVA \_ DXVA** (值。 显示驱动程序在此调用中不会收到任何输入;也就是说，DD RENDERMOCOMPDATA 的 **lpInputData** 成员 \_ 为 **NULL**。 显示驱动程序通过 DD RENDERMOCOMPDATA 的 **lpOutputData** 成员返回证书的长度 \_ 。 **lpOutputData** 指向 DWORD 数据类型。

    显示驱动程序必须使用 COPP IOCTL 与视频微型端口驱动程序通信。 如果视频微型端口驱动程序实现了 [*COPPGetCertificateLength*](./coppgetcertificatelength.md) 示例函数，则 **DdMoCompRender** 回调函数将启动对 *COPPGetCertificateLength*的调用。

4.  若要检索图形硬件使用的证书，VMR 将启动对显示驱动程序提供的 **DdMoCompRender** 回调函数的调用。 在**DdMoCompRender**调用中，DD RENDERMOCOMPDATA 的**dwFunction**成员 \_ 设置为*COPPKeyExchangeFnCode*) 中定义的**DXVA \_ DXVA** (值。 显示驱动程序在此调用中不会收到任何输入;也就是说，DD RENDERMOCOMPDATA 的 **lpInputData** 成员 \_ 为 **NULL**。 DD RENDERMOCOMPDATA 的 **lpBufferInfo** 成员指向 \_ 单个 RGB32 系统内存表面，其中包含显示器驱动程序存储证书所需的空间。 显示驱动程序返回通过 DD RENDERMOCOMPDATA 的 **lpOutputData** 成员生成的128位随机数字 \_ 。

    显示驱动程序必须使用 COPP IOCTL 与视频微型端口驱动程序通信。 如果视频微型端口驱动程序实现了 [*COPPKeyExchange*](./coppkeyexchange.md) 示例函数，则 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数将启动对 *COPPKeyExchange*的调用。

5.  若要将当前视频会话设置为受保护模式，VMR 将启动对显示驱动程序提供的 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数的调用。 在*DdMoCompRender*调用中，DD RENDERMOCOMPDATA 的**dwFunction**成员 \_ 设置为*COPPSequenceStartFnCode*) 中定义的**DXVA \_ DXVA** (值。 DD RENDERMOCOMPDATA 的 **lpInputData** 成员 \_ 通过指向已完成的 [**DXVA \_ COPPSignature**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppsignature) 结构将输入命令和状态序列开始代码传递到显示驱动程序。 显示驱动程序未返回任何输出;也就是说，DD RENDERMOCOMPDATA 的 **lpOutputData** 成员 \_ 为 **NULL**。

    显示驱动程序必须使用 COPP IOCTL 与视频微型端口驱动程序通信。 如果视频微型端口驱动程序实现了 [*COPPSequenceStart*](./coppsequencestart.md) 示例函数，则 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数将启动对 **COPPSequenceStart**的调用。

6.  若要在与 DirectX VA COPP 设备关联的物理连接器上设置保护级别，VMR 将启动对显示驱动程序提供的 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数的调用。 在*DdMoCompRender*调用中，DD RENDERMOCOMPDATA 的**dwFunction**成员 \_ 设置为*COPPCommandFnCode*) 中定义的**DXVA \_ DXVA** (值。 DD RENDERMOCOMPDATA 的 **lpInputData** 成员 \_ 通过指向已完成的 [**DXVA \_ COPPCommand**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppcommand) 结构将输入参数传递到显示驱动程序。 显示驱动程序未返回任何输出;也就是说，DD RENDERMOCOMPDATA 的 **lpOutputData** 成员 \_ 为 **NULL**。

    显示驱动程序必须使用 COPP IOCTL 与视频微型端口驱动程序通信。 如果视频微型端口驱动程序实现了 [*COPPCommand*](./coppcommand.md) 示例函数，则 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数将启动对 *COPPCommand*的调用。

7.  若要检索有关正在使用的物理连接器的保护信息，VMR 会启动对显示驱动程序提供的 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数的调用。 在*DdMoCompRender*调用中，DD RENDERMOCOMPDATA 的**dwFunction**成员 \_ 设置为*COPPQueryStatusFnCode*) 中定义的**DXVA \_ DXVA** (值。 DD RENDERMOCOMPDATA 的 **lpInputData** 成员 \_ 通过指向已完成的 [**DXVA \_ COPPStatusInput**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusinput) 结构将输入参数传递到显示驱动程序。 显示驱动程序通过 DD RENDERMOCOMPDATA 的 **lpOutputData** 成员返回其输出 \_ ; **lpOutputData** 指向 [**DXVA \_ COPPStatusOutput**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusoutput) 结构。

    显示驱动程序必须使用 COPP IOCTL 与视频微型端口驱动程序通信。 如果视频微型端口驱动程序实现了 [*COPPQueryStatus*](./coppquerystatus.md) 示例函数，则 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数将启动对 *COPPQueryStatus*的调用。

8.  当 VMR 不再需要执行更多的 COPP 操作时，将调用显示驱动程序提供的 [*DdMoCompDestroy*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy) 回调函数。 DD MOTIONCOMPCALLBACKS 的 **DestroyMoComp** 成员指向 \_ 回调函数。

    显示驱动程序必须使用 COPP IOCTL 与视频微型端口驱动程序通信。 如果视频微型端口驱动程序实现了 [*COPPCloseVideoSession*](./coppclosevideosession.md) 示例函数，则 **DdMoCompDestroy** 回调函数将启动对 *COPPCloseVideoSession*的调用。

9.  然后，驱动程序会释放 DirectX VA COPP 设备使用的所有资源。

 

