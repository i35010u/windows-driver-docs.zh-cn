---
title: OPM 和 ChangeDisplaySettingsEx
description: OPM 和 ChangeDisplaySettingsEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5be7f93149b95d16c33798bfd6f9742a404faa05
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795003"
---
# <a name="opm-and-changedisplaysettingsex"></a>OPM 和 ChangeDisplaySettingsEx


由于应用程序可以通过调用 Microsoft Win32 **ChangeDisplaySettingsEx** 函数来改变模拟内容保护 (ACP) 级别，因此，显示微型端口驱动程序应确保通过 **ChangeDisplaySettingsEx** 对 ACP 保护类型进行的调整与 **IOPMVideoOutput** 接口所做的调整无关。 换句话说，如果在物理连接器上通过显示微型端口驱动程序的 [**DxgkDdiOPMConfigureProtectedOutput**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output) 函数设置了 ACP 保护类型，则显示微型端口驱动程序不应允许通过 [**IOCTL \_ 视频 \_ 句柄 \_ VIDEOPARAMETERS**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters) 请求禁用物理连接器上的 ACP 保护类型。 请注意，用户模式对 **ChangeDisplaySettingsEx** 的调用将启动 IOCTL \_ 视频 \_ 处理 \_ 对显示微型端口驱动程序的 VIDEOPARAMETERS 请求。

有关 **ChangeDisplaySettingsEx** 函数的详细信息，请参阅 Microsoft Windows SDK 文档。

 

