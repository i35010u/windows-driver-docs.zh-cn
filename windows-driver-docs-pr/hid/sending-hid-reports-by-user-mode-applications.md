---
title: 发送用户模式应用程序通过 HID 报告
description: 发送用户模式应用程序通过 HID 报告
ms.assetid: 265d7393-62be-41ad-8f87-efcfa462de1f
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fc130997ee844e70ab5e11268820ed60b649c6ba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384454"
---
# <a name="sending-hid-reports-by-user-mode-applications"></a>发送用户模式应用程序通过 HID 报告


在用户模式应用程序应使用 WriteFile （如 Microsoft Windows SDK 中所述） 作为其主方法不断将输出报告发送到 HID 集合。 应用程序还可以使用 **HidD\_设置 * * * Xxx*例程以发送输出报告和功能到集合的报表。 但是，应用程序只应使用这些例程可设置集合的当前状态。 某些设备可能不支持**HidD\_SetOutputReport**且会变得无响应，如果使用此例程。

有关详细信息，请参阅[使用 WriteFile](#using-writefile)并[使用 HidD\_SetXxx 例程](#using-hidd-setxxx-routines)。

### <a name="using-writefile"></a>使用 WriteFile

应用程序应使用写入请求发送到 HID 集合输出报告。 在用户模式应用程序创建输出报告后，它可以向使用 WriteFile 集合发送输出报告。

### <a href="" id="using-hidd-setxxx-routines"></a>使用 HidD\_SetXxx 例程

应用程序可以使用以下[HIDClass 支持例程](https://msdn.microsoft.com/library/windows/hardware/ff538865)将 HID 报表发送到 HID 集合：

<a href="" id="hidd-setoutputreport"></a>[**HidD\_SetOutputReport**](https://msdn.microsoft.com/library/windows/hardware/ff539690)  
将输出报告发送到 HID 集合 （Windows XP 和更高版本）。

<a href="" id="hidd-setfeature"></a>[**HidD\_SetFeature**](https://msdn.microsoft.com/library/windows/hardware/ff539684)  
将功能报表发送到 HID 集合。

 

 




