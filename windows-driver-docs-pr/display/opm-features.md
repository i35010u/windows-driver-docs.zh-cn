---
title: OPM 功能
description: OPM 功能
ms.assetid: a2fc9d0c-d85c-484e-8cf2-09b2a84801f8
keywords:
- OPM WDK 显示功能
- OPM WDK 显示、 COPP 和 OPM 比较
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f374d97e66c3699b1b5b18f57c7e0bb72fdb02d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543620"
---
# <a name="opm-features"></a>OPM 功能

OPM 支持所有认证输出保护协议的 (COPP) 功能。 下面介绍一些新 OPM 功能以及一些 OPM 功能如何 COPP 功能进行比较：

-   OPM 要求应用程序登录请求视频时 COPP 不需要应用程序签名的信息从图形驱动程序的请求输出中的信息。

    > [!NOTE]
    > COPP 图形驱动程序相当于 OPM 视频输出。

    COPP 应用程序请求信息从图形驱动程序导致[ **DXVA\_COPPStatusInput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppstatusinput)结构传递给驱动程序。

-   OPM 支持高带宽数字内容保护 (HDCP) 重复字符。 有关 HDCP 重复字符的详细信息，请参阅[HDCP 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。

-   应用程序可以更轻松地支持中 OPM HDCP。 应用程序不需要分析 HDCP 系统可更新性消息 (SRMs) 并确定监视器已被吊销。 有关 HDCP SRMs 详细信息，请参阅[HDCP 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。

-   OPM 使用 X.509 证书和 COPP 使用专有 XML 证书。 COPP 证书格式基于 XML 签名语法和处理规范中的签名格式。 有关 X.509 证书的信息，请参阅[X.509 证书配置文件](https://go.microsoft.com/fwlink/p/?linkid=70416)。

-   COPP 应用程序获取 COPP **IAMCertifiedOutputProtection**通过创建版本 7 或 9 的视频混合使用呈现器的接口 ([*VMR*](https://docs.microsoft.com/windows/desktop/DirectShow/using-the-video-mixing-renderer))，然后将传递 IID\_VMR 筛选器的实现的 IAMCertifiedOutputProtection **iunknown:: Queryinterface**。 OPM 应用程序获得**IOPMVideoOutput**通过传递 HMONITOR 接口或**IDirect3DDevice9**对象传递给**OPMGetVideoOutputsFromHMONITOR**或**OPMGetVideoOutputsFromIDirect3DDevice9Object**分别函数。 有关这些函数和接口的详细信息，请参阅 Microsoft Windows SDK 文档。

-   OPM 支持克隆模式在所有情况下，而 COPP 仅在一个特定的情况下支持克隆模式。

-   OPM 的重新分发控件标记已比 COPP 的重新分发控件标志略有不同的语义 (COPP\_CGMSA\_RedistributionControlRequired)。