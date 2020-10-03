---
title: SIM 双卡
description: SIM 双卡
ms.assetid: 18521fec-c9fb-48d0-9de2-d0482e4807d6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e504e2b06a4f4eb7d8d766197a2bccb20223069
ms.sourcegitcommit: e2de6b9ffb5c7356deb864f9da879533f49b25bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2020
ms.locfileid: "91702658"
---
# <a name="dual-sim"></a>SIM 双卡


Windows Phone 8.1 和更高版本支持双 SIM 双主动 (DSDA) 和双 SIM 双备用 (DSDS) 。 DSDA 允许同时在这两行上进行语音呼叫和短信。 DSDS 允许在这两行上注册，可以从任一行接收/发出调用。 但是，在任何给定时间，语音呼叫中只能有一行。 对于 DSDA 和 DSDS，数据仅限于一行。

Windows Phone 8.1 和更高版本支持 W/G + G。

Windows Phone 8.1 GDR1 增加了对 C + G 的支持。

## <a name="architecture"></a>体系结构


每个 UICC 槽都与执行器关联。 执行器注册到特定的移动电话网络，并处理与移动电话相关的任务，例如拨打和接听电话呼叫和短信。

### <a name="wg--g"></a>W/G + G

对于其无线电类型为 W/G + G 的手机，一个执行器是支持/G 的，一个执行器支持 G。 根据用户选择用于数据行的 UICC 槽，该槽自动与更具功能的 W/G 执行器关联。 以下关系图显示了两个可能的执行器关联，具体取决于用户为数据行选择的 UICC 槽。

![hwcomponents \- dualsim \- logicalview \- 1](images/hwcomponents-dualsim-logicalview.png) ![显示第二个可能的执行器关联的关系图。](images/hwcomponents-dualsim-logicalview-2.png)

### <a name="cg"></a>C + G

对于无线电类型为 C + G 的手机，包含 CDMA UICC 的槽始终使用执行器0。 如果有两个 GSM UICCs，则为数据行选择的 UICC 与执行器0相关联。

## <a name="uicc-swapping"></a>UICC 交换


支持在任一槽中热删除 UICC。 删除 UICC 时，关联的执行器将失去服务，并将显示一个对话框。 不支持热插入 UICCs。 如果在启动后插入了新的 UICC，设备将保持未注册的。

UICC 特定用户设置（如手动 APNs 设置）按 UICC 保存，并在重新插入 UICC 时还原。

## <a name="airplane-mode"></a>飞行模式


打开飞行模式会关闭两行的手机网络。 如果用户在飞行模式下打开了手机网络线路，则会显示 "关闭飞行模式" 提示。

## <a name="pin-lock"></a>PIN 锁定


两个 UICCs 都支持 PIN1、PIN2 和 PUK。

## <a name="sim-toolkit"></a>SIM 工具包


这两个 UICCs 都支持 UTK。 UTK UI 一次只支持一个 UICC。

对于两个 UICC 槽，都支持 UICC REFRESH with RESET UTK 命令。

 

