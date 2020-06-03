---
title: 按使用时间规范化的通信和协作应用程序中用户模式崩溃的次数小于等于基线目标
description: 该度量将 7 天滑动窗口中的遥测数据聚合为通信和协作应用程序在总运行时（以年为单位）内由显卡驱动程序引起的崩溃比率
ms.topic: article
ms.date: 05/11/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5946ec2f3c2754f571a670b24b7be4fb00e875e3
ms.sourcegitcommit: d7b5e6049db3109fdcbe83279875f24f3fa6acdd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "84110255"
---
# <a name="number-of-user-mode-crashes-in-communication-and-collaboration-applications-normalized-by-usage--baseline-goal"></a>按使用时间规范化的通信和协作应用程序中用户模式崩溃的次数小于等于基线目标

## <a name="description"></a>说明

该度量计算在通信和协作应用程序上下文中发生的显示器驱动程序的崩溃次数，并计算具有更新的驱动程序的所有计算机上此类应用程序的运行时。 然后，该度量按累积应用程序运行时（以年为单位）来规范化崩溃计数（HOART 表示命中应用程序运行时）

考虑用于此度量的通信和协作应用程序示例：

* MICROSOFT.SKYPEAPP
* DISCORD.EXE
* SKYPE.EXE
* TEAMVIEWER.EXE
* LYNC.EXE
* WECHAT.EXE
* QQ.EXE
* SLACK.EXE
* KAKAOTALK.EXE
* ZOOM.EXE
* ZOOM
* WHATSAPP.EXE
* LINE.EXE
* YOUCAMSERVICE.EXE
* TELEGRAM.EXE
* VIBER.EXE
* MICROSOFT.SKYPEROOMSYSTEM

对于[按使用时间规范化的通信和协作应用程序中用户模式崩溃的次数小于等于基线目标](https://docs.microsoft.com/windows-hardware/drivers/dashboard/graphics-user-mode-crashes-collaboration-standard)这一度量，这是它在生态系统中的对应项。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众|生态系统|
|时间段|7 天滑动窗口|
|度量标准|通信和协作应用程序运行时的聚合（以年为单位）|
|最小总体数量|10,000 小时的通信和协作应用程序运行时|
|通过标准|每年累积运行时崩溃次数小于等于 1|
|度量 ID|25912731|

## <a name="calculation"></a>计算

该度量将 7 天滑动窗口中的遥测数据聚合为 Microsoft Edge Chromium 在总运行时（以年为单位）内由显卡驱动程序引起的崩溃比率

Microsoft Edge Chromium 崩溃总次数 = 计数（Microsoft Edge Chromium 在具有驱动程序的计算机上的崩溃次数）

Microsoft Edge Chromium 总运行时 = 总和（具有驱动程序的每台计算机的 Microsoft Edge Chromium 运行时）

运行时（以年为单位）= Microsoft Edge Chromium 总运行时 ∗ 60（分钟）∗ 60（小时）∗ 24（天）∗ 365（年）

### <a name="final-calculation"></a>最终计算

按使用时间规范化的 Microsoft Edge Chromium 的崩溃次数 = Microsoft Edge Chromium 崩溃总次数/运行时（年）
