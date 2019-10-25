---
title: 通过用户模式应用程序发送 HID 报表
description: 通过用户模式应用程序发送 HID 报表
ms.assetid: 265d7393-62be-41ad-8f87-efcfa462de1f
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c62e33ad40beef78a42724c9aad0781c3d855a92
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841557"
---
# <a name="sending-hid-reports-by-user-mode-applications"></a>通过用户模式应用程序发送 HID 报表


用户模式应用程序应使用 WriteFile （如 Microsoft Windows SDK 中所述）作为将输出报告持续发送到 HID 集合的主要方法。 应用程序还可以使用 **HidD\_Set * * * Xxx*例程将输出报告和功能报告发送到集合。 但是，应用程序应仅使用这些例程来设置集合的当前状态。 某些设备可能不支持**HidD\_SetOutputReport** ，如果使用此例程，它将停止响应。

有关详细信息，请参阅[使用 WriteFile](#using-writefile)和[使用 HidD\_SetXxx 例程](#using-hidd-setxxx-routines)。

### <a name="using-writefile"></a>使用 WriteFile

应用程序应使用写入请求将输出报告发送到 HID 集合。 用户模式应用程序创建输出报表后，可以使用 WriteFile 将输出报告发送到集合。

### <a href="" id="using-hidd-setxxx-routines"></a>使用 HidD\_SetXxx 例程

应用程序可以使用以下[HIDClass 支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)将 hid 报告发送到 hid 集合：

<a href="" id="hidd-setoutputreport"></a>[**HidD\_SetOutputReport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setoutputreport)  
将输出报告发送到 HID 集合（Windows XP 及更高版本）。

<a href="" id="hidd-setfeature"></a>[**HidD\_SetFeature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setfeature)  
向 HID 集合发送功能报表。

 

 




