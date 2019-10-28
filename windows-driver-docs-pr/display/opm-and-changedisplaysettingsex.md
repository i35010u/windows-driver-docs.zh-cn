---
title: OPM 和 ChangeDisplaySettingsEx
description: OPM 和 ChangeDisplaySettingsEx
ms.assetid: 973a8481-4d9a-4272-9138-666c6e41ad89
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 257b5407c5e7bfa10d5fed56669cb5be3ab70bc5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840497"
---
# <a name="opm-and-changedisplaysettingsex"></a>OPM 和 ChangeDisplaySettingsEx


由于应用程序可以通过调用 Microsoft Win32 **ChangeDisplaySettingsEx**函数来改变模拟内容保护（ACP）级别，因此显示微型端口驱动程序应确保通过**ChangeDisplaySettingsEx**独立于由**IOPMVideoOutput**接口进行的调整。 换句话说，如果在物理连接器上通过显示微型端口驱动程序的[**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)函数设置了 ACP 保护类型，则显示微型端口驱动程序不应允许禁用 ACP 保护类型通过[**IOCTL\_视频\_处理\_VIDEOPARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)请求的物理连接器。 请注意，用户模式对**ChangeDisplaySettingsEx**的调用将启动 IOCTL\_视频\_处理显示微型端口驱动程序\_VIDEOPARAMETERS 请求。

有关**ChangeDisplaySettingsEx**函数的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 





