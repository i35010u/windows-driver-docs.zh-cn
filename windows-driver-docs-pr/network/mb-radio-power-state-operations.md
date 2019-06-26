---
title: MB 发射功率状态操作
description: MB 发射功率状态操作
ms.assetid: 9b745ff3-c00b-4a43-9bf3-52f9bf61e062
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aad2618143ccf6d88ab957f66e82ce46fce813a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374033"
---
# <a name="mb-radio-power-state-operations"></a>MB 发射功率状态操作


本主题介绍用于设置和读取 MB 设备的无线电电源状态的操作。 WWAN 中的以下值\_单选枚举描述由 MB 服务支持的两个电源状态：

-   *WwanRadioOn*: 单选上，加载堆栈，并在设备是否能够执行移动电话的过程，以及解答主机命令。

-   *WwanRadioOff*: 单选处于关闭状态。 在此状态下，设备有电源，并应响应的命令。 但是没有与单选相关的操作应执行除主机命令，以启用单选。

单选电源状态控制 MB 服务或硬件开关 （如果存在）。

请注意单选电源状态可能会更改在便携式计算机 （便携式计算机） 上由于以下原因：

-   大多数便携式计算机配备有可用于启用和禁用单选的交换机。 有效地关闭按钮切掉 MB 模块从计算机底板上的幂。 最终，单选已完全关闭电源。

-   MB 服务可能会将命令发送到要置于低功耗状态以节省电量或避免与环境无线电干扰无线电的微型端口驱动程序 (如在飞机上)。

有关单选电源状态操作的详细信息，请参阅[OID\_WWAN\_单选\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-radio-state)。

 

 





