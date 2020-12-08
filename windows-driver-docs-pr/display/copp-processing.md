---
title: COPP 处理
description: COPP 处理
keywords:
- DirectX 视频加速 WDK Windows 2000 显示，COPP
- 视频加速 WDK DirectX，COPP
- VA WDK DirectX，COPP
- 认证的输出保护协议 WDK DirectX VA
- 复制保护 WDK COPP
- 视频复制保护 WDK COPP
- COPP WDK DirectX VA
- 受保护的视频 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7996e7c43c315f8ae7ab4ea429a858133c36a9ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786377"
---
# <a name="copp-processing"></a>COPP 处理


## <span id="ddk_certified_output_protection_protocol_processing_gg"></span><span id="DDK_CERTIFIED_OUTPUT_PROTECTION_PROTOCOL_PROCESSING_GG"></span>


本部分仅适用于 Microsoft Windows Server 2003 Service Pack 1 (SP1) 和更高版本，以及 Windows XP Service Pack 2 (SP2) 和更高版本。

认证的输出保护协议 (COPP) 设备驱动程序接口 (DDI) 将 DirectX 视频加速功能扩展到 (VA) ，以支持由图形适配器的各种连接器输出的视频的复制保护。 COPP DDI 是 (*VMR*) 和视频微型端口驱动程序的视频混合呈现器之间的接口。 COPP DDI 映射到现有 DirectDraw 和 DirectX VA DDI。 不能通过 **IAMVideoAccelerator** 接口访问 DDI。 应用程序可以通过 **IAMCertifiedOutputProtection** 接口访问 DDI。

有关 **IAMCertifiedOutputProtection** 和 **IAMVideoAccelerator** 接口的详细信息，请参阅最新的 DirectX 软件开发工具包 (SDK) 文档。

如果视频微型端口驱动程序支持在应用程序和驱动程序之间传递受保护的命令和状态，VMR 将启动对驱动程序的调用，以创建 DirectX VA COPP 设备。

以下主题介绍 COPP DDI 和如何支持 COPP：

[COPP 简介](introduction-to-copp.md)

[将 COPP DDI 映射到 DirectDraw 和 DirectX VA](mapping-the-copp-ddi-to-directdraw-and-directx-va.md)

[COPP 的示例函数](sample-functions-for-copp.md)

[从 COPP 函数返回错误代码](returning-error-codes-from-copp-functions.md)

[执行 COPP 操作](performing-copp-operations.md)

[COPP 实施提示和要求](implementation-tips-and-requirements-for-copp.md)

 

 





