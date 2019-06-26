---
title: COPP 和 ChangeDisplaySettingsEx
description: COPP 和 ChangeDisplaySettingsEx
ms.assetid: 5c729bfd-0758-4de5-9e81-a3279f8aab56
keywords:
- 复制保护 WDK COPP ChangeDisplaySettingsEx
- 视频复制保护 WDK COPP ChangeDisplaySettingsEx
- COPP WDK DirectX VA ChangeDisplaySettingsEx
- 受保护视频 WDK COPP ChangeDisplaySettingsEx
- ChangeDisplaySettingsEx
- 模拟内容保护 WDK COPP
- ACP 保护类型 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e14718f2b7a0593851e3a9e03c50f11c8d8663f6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370269"
---
# <a name="copp-and-changedisplaysettingsex"></a>COPP 和 ChangeDisplaySettingsEx


## <span id="ddk_copp_and_changedisplaysettingsex_gg"></span><span id="DDK_COPP_AND_CHANGEDISPLAYSETTINGSEX_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。**

因为应用程序可以更改模拟内容保护 (ACP) 级别通过调用 Microsoft Win32 **ChangeDisplaySettingsEx**函数，该视频的微型端口驱动程序应确保通过键入 ACP 保护所做的调整**ChangeDisplaySettingsEx**独立于进行的调整**IAMCertifiedOutputProtection**接口。 换而言之，如果通过微型端口驱动程序的物理连接器上设置的 ACP 保护类型[ *COPPCommand* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)函数，该视频的微型端口驱动程序不应允许禁用 ACP通过物理连接器上的保护类型[ **IOCTL\_视频\_处理\_VIDEOPARAMETERS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)请求。 请注意该用户模式下调用**ChangeDisplaySettingsEx**启动 IOCTL\_视频\_处理\_VIDEOPARAMETERS 请求到微型端口驱动程序。

有关详细信息**ChangeDisplaySettingsEx**函数中，请参阅 Windows SDK 文档。

 

 





