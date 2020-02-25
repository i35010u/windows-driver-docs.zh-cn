---
title: Microsoft 蓝牙测试平台
description: 支持蓝牙测试平台（BTP）的硬件（音频）。
ms.assetid: a6beeecb-5967-4e08-bfe2-b8aae26861ad
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: 9d7a525e57dcee8187c3c98194a023e10ea85379
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528911"
---
# <a name="audio-capable-peripheral-radios"></a>支持音频的外设无线收发器 #

蓝牙测试平台（BTP） Traduci 板需要一个12针连接器来与任何收音机模块通信。 此处列出的音频无线电和取得突破采用收音机模块，并将所需的 pin 分解为所需的12针布局。

| 广播 | 功能 | 参数 |
| --- | --- | --- |
| RN52 | 基本速率（BR）广播 | rn52 （例如 RunPairingTests rn52） |

## <a name="audio-sled-rn52-radio"></a>音频滑板（RN52 收音机） ##

RN52 是来自漫游网络的基本费率（BR），可以表现为音频外设，如扬声器或耳机。 目前计划在即将推出的 BTP 音频测试中支持。 可以通过[**微芯片**](https://www.microchip.com/wwwproducts/en/RN52)中的 RN52 页找到详细信息。 此滑板打破了无线电的音频输出数据，并将其路由到 Traduci 上的音频编解码器和音频处理 FPGA，以帮助验证。

### <a name="rn52-radio"></a>RN52 广播 ###

![RN52 收音机的照片](images/RN52.png)

### <a name="rn52-radio-on-btp-compatible-sled"></a>BTP 兼容的滑板上的 RN52 收音机 ###

![滑板上 RN52 收音机的照片](images/Traduci_and_RN52.jpg)

> [!NOTE]
> RN52 收音机**只能**插入标记为 "JA" 的 Traduci 板12针端口。

- UART 数据连接与 AT 命令用于配置软件
- 支持 SPP、A2DP、HFP 和 AVRCP 配置文件
- 版本3.0 音频模块
- 完全认证类 2 BR 蓝牙 2.1 + EDR
- 小型外形规格，低功率，surface 装模块
