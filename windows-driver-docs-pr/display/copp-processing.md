---
title: COPP 处理
description: COPP 处理
ms.assetid: c9ff0fd3-c063-4450-ae66-54153b3dc53c
keywords:
- DirectX 视频加速 WDK Windows 2000 显示 COPP
- 视频加速 WDK DirectX COPP
- VA WDK DirectX COPP
- 认证的输出保护协议 WDK DirectX VA
- 复制保护 WDK COPP
- 视频复制保护 WDK COPP
- COPP WDK DirectX VA
- 受保护视频 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53caf237ebf422fbaf0036ad77ada0613fd6624e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526631"
---
# <a name="copp-processing"></a>COPP 处理


## <span id="ddk_certified_output_protection_protocol_processing_gg"></span><span id="DDK_CERTIFIED_OUTPUT_PROTECTION_PROTOCOL_PROCESSING_GG"></span>


本部分仅适用于 Microsoft Windows Server 2003 Service Pack 1 (SP1) 和更高版本和 Windows XP Service Pack 2 (SP2) 和更高版本。

认证的输出保护协议 (COPP) 设备驱动程序接口 (DDI) 扩展了 DirectX 视频加速 (VA) 以支持复制保护的视频，它是由各种图形适配器的连接器的输出。 COPP DDI 是视频混合使用呈现器之间的接口 (*VMR*) 和视频的微型端口驱动程序。 COPP DDI 映射到现有的 DirectDraw 和 DirectX VA DDI。 DDI 不是可通过访问**IAMVideoAccelerator**接口。 DDI 是通过应用程序可以访问**IAMCertifiedOutputProtection**接口。

有关详细信息**IAMCertifiedOutputProtection**并**IAMVideoAccelerator**接口，请参阅最新的 DirectX 软件开发工具包 (SDK) 文档。

如果视频的微型端口驱动程序支持应用程序和驱动程序之间的受保护的命令和状态传递，VMR 将启动创建 DirectX VA COPP 设备驱动程序调用。

以下主题介绍了 COPP DDI 以及如何支持 COPP:

[COPP 简介](introduction-to-copp.md)

[映射到 DirectDraw 和 DirectX VA COPP DDI](mapping-the-copp-ddi-to-directdraw-and-directx-va.md)

[COPP 的示例函数](sample-functions-for-copp.md)

[从 COPP 函数返回错误代码](returning-error-codes-from-copp-functions.md)

[执行 COPP 操作](performing-copp-operations.md)

[实现技巧和 COPP 的要求](implementation-tips-and-requirements-for-copp.md)

 

 





