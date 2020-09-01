---
title: MB 发射功率状态操作
description: MB 发射功率状态操作
ms.assetid: 9b745ff3-c00b-4a43-9bf3-52f9bf61e062
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98635698eba41fbdef721d7f0a1b5e9920fcea47
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207287"
---
# <a name="mb-radio-power-state-operations"></a>MB 发射功率状态操作


本主题介绍用于设置和读取 MB 设备的无线电电源状态 (s) 的操作。 WWAN 无线枚举中的以下值 \_ 描述了 MB 服务支持的两种电源状态：

-   *WwanRadioOn*：无线电已打开，已加载堆栈，并且设备能够执行手机网络过程以及应答主机命令。

-   *WwanRadioOff*：无线电已关闭。 在此状态下，设备已通电并应响应命令。 但不应执行与广播相关的操作，除非主机命令打开收音机。

无线电电源状态由 MB 服务控制，如果) 存在，则由硬件开关 (。

请注意，由于以下原因，计算机上的无线电电源状态在便携式计算机 () 可能会发生变化：

-   大多数便携式计算机配有可用于打开和关闭无线电的开关。 关闭按钮会有效地切断从计算机底板到 MB 模块的电源。 最终，无线电完全关机。

-   MB 服务可能会将命令发送到微型端口驱动程序，以使无线电进入低功耗状态以节省电源，或避免与环境的无线电干扰 (例如在飞机) 上。

有关无线电电源状态操作的详细信息，请参阅 [OID \_ WWAN \_ 无线电 \_ 状态](./oid-wwan-radio-state.md)。

 

