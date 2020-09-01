---
title: COPP 和 ChangeDisplaySettingsEx
description: COPP 和 ChangeDisplaySettingsEx
ms.assetid: 5c729bfd-0758-4de5-9e81-a3279f8aab56
keywords:
- 复制保护 WDK COPP，ChangeDisplaySettingsEx
- 视频复制保护 WDK COPP，ChangeDisplaySettingsEx
- COPP WDK DirectX VA，ChangeDisplaySettingsEx
- 受保护的视频 WDK COPP，ChangeDisplaySettingsEx
- ChangeDisplaySettingsEx
- 模拟内容保护 WDK COPP
- ACP protection 类型 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fcf595ebb2bb0de53fa528407a0fdc3fab029bd
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067336"
---
# <a name="copp-and-changedisplaysettingsex"></a>COPP 和 ChangeDisplaySettingsEx


## <span id="ddk_copp_and_changedisplaysettingsex_gg"></span><span id="DDK_COPP_AND_CHANGEDISPLAYSETTINGSEX_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

由于应用程序可以通过调用 Microsoft Win32 **ChangeDisplaySettingsEx** 函数来改变模拟内容保护 (ACP) 级别，因此，视频微型端口驱动程序应确保通过 **ChangeDisplaySettingsEx** 对 ACP 保护类型进行的调整与 **IAMCertifiedOutputProtection** 接口所做的调整无关。 换句话说，如果通过视频微型端口驱动程序的 [*COPPCommand*](./coppcommand.md) 函数在物理连接器上设置 ACP 保护类型，则视频微型端口驱动程序不应允许通过 [**IOCTL \_ 视频 \_ 句柄 \_ VIDEOPARAMETERS**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters) 请求禁用物理连接器上的 ACP 保护类型。 请注意，用户模式对 **ChangeDisplaySettingsEx** 的调用将启动 IOCTL \_ 视频 \_ 处理 \_ 对视频微型端口驱动程序的 VIDEOPARAMETERS 请求。

有关 **ChangeDisplaySettingsEx** 函数的详细信息，请参阅 Windows SDK 文档。

 

