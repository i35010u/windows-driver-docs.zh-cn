---
title: 配置受保护输出
description: 配置受保护输出
ms.assetid: ff740b37-6e4a-4243-8e83-97dc2a46e3f1
keywords:
- OPM WDK 显示中，配置受保护的输出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5df5f4d3a89536c83e34ee5074a11a61f20cebf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376769"
---
# <a name="configuring-a-protected-output"></a>配置受保护输出


显示微型端口驱动程序可以接收请求，以配置受保护与图形适配器的物理输出连接器相关联的输出。 显示微型端口驱动程序[ **DxgkDdiOPMConfigureProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559701)函数传递一个指向[ **DXGKMDT\_OPM\_配置\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff560849)结构，它指定如何配置受保护的输出。 **GuidSetting**并**abParameters** DXGKMDT 成员\_OPM\_配置\_参数指定配置请求。

**请注意**  之前**DxgkDdiOPMConfigureProtectedOutput**返回时，显示微型端口驱动程序必须验证一个密钥加密块链接 (CBC)-是的模式消息身份验证代码 (OMAC)中指定**omac** DXGKMDT 成员\_OPM\_配置\_参数是否正确。 有关验证 OMAC 的详细信息，请参阅[OMAC 1 算法](https://go.microsoft.com/fwlink/p/?linkid=70417)。 此外必须验证该驱动程序中的序列号，指定**ulSequenceNumber** DXGKMDT 成员\_OPM\_配置\_参数匹配序列号驱动程序当前已存储。 然后，该驱动程序必须递增存储的序列号。

 

显示微型端口驱动程序应支持以下配置请求：

-   [保护级别设置为受保护的输出](setting-the-protection-level-for-a-protected-output.md)

-   [配置保护的视频信号](configuring-protection-for-the-video-signal.md)

-   [设置 HDCP SRM 版本](setting-the-hdcp-srm-version.md)

 

 





