---
title: 支持 WBDI 驱动程序中的安全通道
description: 支持 WBDI 驱动程序中的安全通道
ms.assetid: 1b4532f4-18ee-4c65-9373-2ca635d2f40d
keywords:
- 生物识别驱动程序 WDK，安全通道
- 安全通道 WDK 生物识别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86d094897584be04bf2efe022930ed743b94b0e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548225"
---
# <a name="supporting-secure-channels-in-wbdi-drivers"></a>支持 WBDI 驱动程序中的安全通道


若要在 WBDI 驱动程序支持在主机和设备之间的安全通道，必须将封装在驱动程序中与安全相关的功能。 然后，该驱动程序管理的安全通道。 当驱动程序通过 Windows 生物识别服务 (WBS) 到了示例数据时，数据必须是未加密。 如有必要，WBS 中插件的供应商提供引擎可以设置 web 服务的安全通道。

安全注意事项应是透明的 WBF 的应用程序。

 

 





