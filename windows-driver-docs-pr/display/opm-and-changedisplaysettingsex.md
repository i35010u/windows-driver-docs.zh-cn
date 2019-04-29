---
title: OPM 和 ChangeDisplaySettingsEx
description: OPM 和 ChangeDisplaySettingsEx
ms.assetid: 973a8481-4d9a-4272-9138-666c6e41ad89
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a6fc517b9264785635963dcf5ec839874fce350
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379859"
---
# <a name="opm-and-changedisplaysettingsex"></a>OPM 和 ChangeDisplaySettingsEx


因为应用程序可以更改模拟内容保护 (ACP) 级别通过调用 Microsoft Win32 **ChangeDisplaySettingsEx**函数，显示微型端口驱动程序应确保调整到 ACP 保护类型通过**ChangeDisplaySettingsEx**独立于进行的调整**IOPMVideoOutput**接口。 换而言之，如果通过显示微型端口驱动程序的物理连接器上设置的 ACP 保护类型[ **DxgkDdiOPMConfigureProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559701)函数，应显示微型端口驱动程序不允许禁用通过物理连接器上的 ACP 保护类型[ **IOCTL\_视频\_处理\_VIDEOPARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff567805)请求。 请注意该用户模式下调用**ChangeDisplaySettingsEx**启动 IOCTL\_视频\_处理\_VIDEOPARAMETERS 请求到显示微型端口驱动程序。

有关详细信息**ChangeDisplaySettingsEx**函数中，请参阅 Microsoft Windows SDK 文档。

 

 





