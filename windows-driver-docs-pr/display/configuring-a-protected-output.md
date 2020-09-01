---
title: 配置受保护输出
description: 配置受保护输出
ms.assetid: ff740b37-6e4a-4243-8e83-97dc2a46e3f1
keywords:
- OPM WDK 显示，配置受保护的输出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d2e65ea64f43836f4bb60d5b8b89ff528989363
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064908"
---
# <a name="configuring-a-protected-output"></a>配置受保护输出


显示微型端口驱动程序可以接收请求，以配置与图形适配器的物理输出连接器关联的受保护的输出。 将向显示微型端口驱动程序的 [**DxgkDdiOPMConfigureProtectedOutput**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output) 函数传递一个指向 [**DXGKMDT \_ OPM \_ 配置 \_ 参数**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters) 结构的指针，该结构指定如何配置受保护的输出。 DXGKMDT OPM CONFIGURE 参数的 **guidSetting** 和 **abParameters** 成员 \_ \_ \_ 指定配置请求。

**注意**   在**DxgkDdiOPMConfigureProtectedOutput**返回之前，显示微型端口驱动程序必须验证 (CBC) 模式消息身份验证代码的单密钥密码块链是否 (OMAC) ，该代码在**omac** DXGKMDT \_ OPM \_ 配置参数的 OMAC 成员中指定 \_ 。 有关验证 OMAC 的详细信息，请参阅 [OMAC 算法](https://go.microsoft.com/fwlink/p/?linkid=70417)。 驱动程序还必须验证在 DXGKMDT OPM 配置参数的 **ulSequenceNumber** 成员中指定的序列号 \_ 是否 \_ \_ 与驱动程序当前已存储的序列号匹配。 然后，该驱动程序必须递增存储的序列号。

 

显示微型端口驱动程序应支持以下配置请求：

-   [设置受保护输出的保护级别](setting-the-protection-level-for-a-protected-output.md)

-   [为视频信号配置保护](configuring-protection-for-the-video-signal.md)

-   [设置 HDCP SRM 版本](setting-the-hdcp-srm-version.md)

 

