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
ms.openlocfilehash: 0bcde3a67ea1038eb92ffa3100088852ac8a7bff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346917"
---
# <a name="copp-and-changedisplaysettingsex"></a>COPP 和 ChangeDisplaySettingsEx


## <span id="ddk_copp_and_changedisplaysettingsex_gg"></span><span id="DDK_COPP_AND_CHANGEDISPLAYSETTINGSEX_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。**

因为应用程序可以更改模拟内容保护 (ACP) 级别通过调用 Microsoft Win32 **ChangeDisplaySettingsEx**函数，该视频的微型端口驱动程序应确保通过键入 ACP 保护所做的调整**ChangeDisplaySettingsEx**独立于进行的调整**IAMCertifiedOutputProtection**接口。 换而言之，如果通过微型端口驱动程序的物理连接器上设置的 ACP 保护类型[ *COPPCommand* ](https://msdn.microsoft.com/library/windows/hardware/ff539642)函数，该视频的微型端口驱动程序不应允许禁用 ACP通过物理连接器上的保护类型[ **IOCTL\_视频\_处理\_VIDEOPARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff567805)请求。 请注意该用户模式下调用**ChangeDisplaySettingsEx**启动 IOCTL\_视频\_处理\_VIDEOPARAMETERS 请求到微型端口驱动程序。

有关详细信息**ChangeDisplaySettingsEx**函数中，请参阅 Windows SDK 文档。

 

 





