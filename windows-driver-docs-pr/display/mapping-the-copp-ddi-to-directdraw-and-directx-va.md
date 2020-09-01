---
title: 将 COPP DDI 映射到 DirectDraw 和 DirectX VA
description: 将 COPP DDI 映射到 DirectDraw 和 DirectX VA
ms.assetid: 737dabab-39f0-44fd-9d34-56d812ffde88
keywords:
- 复制保护 WDK COPP，映射 COPP DDI
- 视频复制保护 WDK COPP，映射 COPP DDI
- COPP WDK DirectX VA，映射 COPP DDI
- 受保护的视频 WDK COPP，映射 COPP DDI
- 映射 COPP DDI WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f7cdc1e26d6b858483e64d774ced84a803cf3fa
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065420"
---
# <a name="mapping-the-copp-ddi-to-directdraw-and-directx-va"></a>将 COPP DDI 映射到 DirectDraw 和 DirectX VA


## <span id="ddk_mapping_the_copp_ddi_to_directdraw_and_directx_va_gg"></span><span id="DDK_MAPPING_THE_COPP_DDI_TO_DIRECTDRAW_AND_DIRECTX_VA_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

必须通过 DirectDraw 的 [运动补偿回调函数](motion-compensation-callbacks.md) 访问 COPP 功能，可以将 [COPP DDI](sample-functions-for-copp.md) 映射到该函数。 由于 COPP DDI 是在视频微型端口驱动程序中实现的，因此显示驱动程序必须 [使用 COPP IOCTLs 与视频微型端口驱动程序通信](communicating-ioctls-to-the-video-miniport-driver.md)。

COPP DDI 可映射到运动补偿回调函数，因为它们不使用类型化参数 (也就是说，其单个参数是指向结构) 的指针。 换句话说，传递给运动补偿回调函数的单个参数中的信息可根据其信息类型进行处理。

例如，如果将 **DXVA \_ COPPGetCertificateLengthFnCode**类型的信息传递到 [*DdMoCompRender*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 函数，则 *DdMoCompRender* 可以启动对 COPPGetCertificateLength DDI 的 [*COPP*](./coppgetcertificatelength.md) 函数的调用，以查询图形硬件使用的证书的长度（以字节为单位）。 但是，如果 **将 DXVA \_ COPPSequenceStartFnCode**类型的信息传递给 *DdMoCompRender* ，则 *DdMoCompRender* 可以启动对 COPPSequenceStart DDI 的 [*COPP*](./coppsequencestart.md) 函数的调用，以指示当前视频会话上受保护的命令和状态序列的开头。

以下主题介绍了如何将 COPP DDI 映射到运动补偿回调函数：

[DirectX VA COPP 设备](directx-va-copp-device.md)

[从用户模式组件调用 COPP DDI](calling-the-copp-ddi-from-a-user-mode-component.md)

[从显示驱动程序调用 COPP DDI](calling-the-copp-ddi-from-the-display-driver.md)

 

