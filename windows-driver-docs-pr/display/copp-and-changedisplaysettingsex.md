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
ms.openlocfilehash: 4d38267a5945ba880cadd83a85bbf571b7ab722b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839039"
---
# <a name="copp-and-changedisplaysettingsex"></a>COPP 和 ChangeDisplaySettingsEx


## <span id="ddk_copp_and_changedisplaysettingsex_gg"></span><span id="DDK_COPP_AND_CHANGEDISPLAYSETTINGSEX_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

由于应用程序可以通过调用 Microsoft Win32 **ChangeDisplaySettingsEx**函数来改变模拟内容保护（ACP）级别，因此视频微型端口驱动程序应确保通过**ChangeDisplaySettingsEx**独立于**IAMCertifiedOutputProtection**接口进行的调整。 换句话说，如果通过视频微型端口驱动程序的[*COPPCommand*](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)函数在物理连接器上设置了 ACP 保护类型，则视频微型端口驱动程序不应允许通过[**IOCTL\_视频\_处理\_VIDEOPARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)请求。 请注意，用户模式对**ChangeDisplaySettingsEx**的调用将启动 IOCTL\_视频\_处理视频微型端口驱动程序\_VIDEOPARAMETERS 请求。

有关**ChangeDisplaySettingsEx**函数的详细信息，请参阅 Windows SDK 文档。

 

 





