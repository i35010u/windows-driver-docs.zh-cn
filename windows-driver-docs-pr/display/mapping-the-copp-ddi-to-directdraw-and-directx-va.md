---
title: 将 COPP DDI 映射到 DirectDraw 和 DirectX VA
description: 将 COPP DDI 映射到 DirectDraw 和 DirectX VA
ms.assetid: 737dabab-39f0-44fd-9d34-56d812ffde88
keywords:
- 复制保护 WDK COPP，映射 COPP DDI
- 视频复制保护 WDK COPP，映射 COPP DDI
- COPP WDK DirectX VA，映射 COPP DDI
- 受保护视频 WDK COPP 映射 COPP DDI
- 映射 COPP DDI WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5793feb0cc669e966f9cc29ffddfccaf17a427c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564277"
---
# <a name="mapping-the-copp-ddi-to-directdraw-and-directx-va"></a>将 COPP DDI 映射到 DirectDraw 和 DirectX VA


## <span id="ddk_mapping_the_copp_ddi_to_directdraw_and_directx_va_gg"></span><span id="DDK_MAPPING_THE_COPP_DDI_TO_DIRECTDRAW_AND_DIRECTX_VA_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。**

必须通过访问 COPP 功能[动作补偿回调函数](motion-compensation-callbacks.md)的 DirectDraw，向其[COPP DDI](sample-functions-for-copp.md)可以映射。 显示驱动程序由于 COPP DDI 微型端口驱动程序中实现，必须[微型端口驱动程序与通信使用 COPP Ioctl](communicating-ioctls-to-the-video-miniport-driver.md)。

COPP DDI 可以映射到运动补偿回调函数，因为它们不使用类型化的参数 （即，其单个参数是指向一个结构的指针）。 换而言之，可以根据其信息类型处理传递给运动补偿回调函数的单个参数中的信息。

例如，如果**DXVA\_COPPGetCertificateLengthFnCode**的类型信息传递给[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)函数，然后*DdMoCompRender*可以向发起呼叫[ *COPPGetCertificateLength* ](https://msdn.microsoft.com/library/windows/hardware/ff539644)查询图形所使用的证书以字节为单位的长度 COPP DDI 函数硬件。 但是，如果**DXVA\_COPPSequenceStartFnCode**的类型信息传递给*DdMoCompRender*相反，然后*DdMoCompRender*可以启动对的调用[ *COPPSequenceStart* ](https://msdn.microsoft.com/library/windows/hardware/ff540421) COPP DDI 以指示当前的视频会话上受保护的命令和状态序列开头的函数。

以下主题介绍了如何 COPP DDI 映射到运动补偿回调函数：

[DirectX VA COPP 设备](directx-va-copp-device.md)

[从用户模式组件调用 COPP DDI](calling-the-copp-ddi-from-a-user-mode-component.md)

[从显示驱动程序调用 COPP DDI](calling-the-copp-ddi-from-the-display-driver.md)

 

 





