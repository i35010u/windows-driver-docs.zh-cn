---
title: OPM 功能
description: OPM 功能
ms.assetid: a2fc9d0c-d85c-484e-8cf2-09b2a84801f8
keywords:
- OPM WDK 显示，功能
- OPM WDK 显示、COPP 和 OPM 比较
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92208d4b15d29032377b4e49b07c74b1205e8335
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840494"
---
# <a name="opm-features"></a>OPM 功能

OPM 支持所有认证的输出保护协议（COPP）功能。 下面介绍了一些新的 OPM 功能以及某些 OPM 功能与 COPP 功能的比较：

-   OPM 要求应用程序对来自视频输出的信息的请求进行签名，而 COPP 不需要应用程序对图形驱动程序中的信息请求进行签名。

    > [!NOTE]
    > COPP 图形驱动程序与 OPM 视频输出等效。

    COPP 应用程序通过导致[**DXVA\_COPPStatusInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusinput)结构传递到驱动程序，从图形驱动程序请求信息。

-   OPM 支持高带宽数字内容保护（HDCP）中继器。 有关 HDCP 中继器的详细信息，请参阅[Hdcp 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。

-   应用程序可以更轻松地支持 OPM 中的 HDCP。 应用程序无需分析 HDCP 系统 Renewability 消息（SRMs）并确定是否已吊销监视器。 有关 HDCP SRMs 的详细信息，请参阅[Hdcp 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。

-   OPM 使用 x.509 证书，COPP 使用专有 XML 证书。 COPP 证书格式基于 XML 签名语法和处理规范中的签名格式。 有关 x.509 证书的信息，请参阅[X.509 证书配置文件](https://go.microsoft.com/fwlink/p/?linkid=70416)。

-   COPP 应用程序通过创建视频混合呈现器（[*VMR*](https://docs.microsoft.com/windows/desktop/DirectShow/using-the-video-mixing-renderer)）的7或9版，然后将 IID\_IAMCertifiedOutputProtection 传递到 VMR 筛选器的实现 **，来获取 COPP IAMCertifiedOutputProtection 接口IUnknown：： QueryInterface**。 OPM 应用程序通过将 HMONITOR 或**IDirect3DDevice9**对象传递到**OPMGetVideoOutputsFromHMONITOR**或**OPMGetVideoOutputsFromIDirect3DDevice9Object**函数来获取**IOPMVideoOutput**接口分别. 有关这些函数和接口的详细信息，请参阅 Microsoft Windows SDK 文档。

-   在所有情况下，OPM 都支持 clone 模式，而 COPP 仅在一种特定情况下支持克隆模式。

-   OPM 的再分发控制标志的语义略有不同，COPP 的再分发控制标志（COPP\_CGMSA\_RedistributionControlRequired）。