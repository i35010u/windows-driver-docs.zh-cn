---
title: SIM 双卡
description: SIM 双卡
ms.assetid: 18521fec-c9fb-48d0-9de2-d0482e4807d6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba7b3aa144a62d7465ecffcaa45f61d209f5d703
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372717"
---
# <a name="dual-sim"></a>SIM 双卡


Windows Phone 8.1 及更高版本支持双 SIM 双 Active (DSDA) 和双 SIM 双待机状态 (DSDS)。 DSDA 允许语音呼叫和短信这两个行上同时。 DSDS 允许注册这两个行，并调用可从任意一条线收到/进行。 但是，只有一个行可以是在任何给定时间语音呼叫。 有关 DSDA 和 DSDS，数据被限制为只有一个行。

Windows Phone 8.1 和更高版本支持 W/G + g。

Windows Phone 8.1 GDR1 添加了支持的 C + g。

## <a name="architecture"></a>体系结构


每个 UICC 槽是与执行器相关联。 执行器将会注册到特定的移动电话网络，和句柄移动电话网络相关的任务，例如拨打和接听电话呼叫和短信。

### <a name="wg--g"></a>W/G + G

适用于手机的无线电类型 W/G + G，一个执行器是 W/G 支持和一个执行器是 G 支持。 具体取决于用户选择要用于数据行的 UICC 槽，该槽会自动与能力更强的 W/G 执行器关联。 下图显示两个可能的执行器关联，具体取决于用户选择的数据行的 UICC 槽。

![hwcomponents\-dualsim\-logicalview\-1](images/hwcomponents-dualsim-logicalview.png)![hwcomponents\-dualsim\-logicalview\-2](images/hwcomponents-dualsim-logicalview-2.png)

### <a name="cg"></a>C+G

对于具有单选键入 C + G 的电话，始终包含 CDMA UICC 的槽使用执行器 0。 如果有两个 GSM UICCs，为数据行选择 UICC 是与执行器 0 相关联。

有关配置 C + G 的详细信息，请参阅[配置 C + G 双 SIM 设置](https://msdn.microsoft.com/library/windows/hardware/dn757414)。

## <a name="uicc-swapping"></a>UICC 交换


支持热删除 UICC 在任一槽中。 UICC 删除关联的执行器将会丢失服务，并将显示一个对话框。 不支持热 UICCs 插入。 如果新 UICC 插入启动后，设备将保持未注册。

UICC 特定用户设置，如手动 APNs 设置每 UICC 保存并重新插入 UICC 时还原。

## <a name="airplane-mode"></a>飞行模式


开启飞行模式将关闭这两个线条的移动电话网络。 如果用户启用蜂窝电话线路在飞行模式下，将显示在提示符下，若要关闭飞行模式。

## <a name="pin-lock"></a>PIN 锁定


这两个 UICCs 支持 PIN1、 pin2 码和 PUK。

## <a name="sim-toolkit"></a>SIM 工具包


这两个 UICCs 支持 UTK。 一次只有一个 UICC 上支持 UTK UI。

这两个 UICC 槽被支持使用重置 UTK 命令 UICC 刷新。

 

 





