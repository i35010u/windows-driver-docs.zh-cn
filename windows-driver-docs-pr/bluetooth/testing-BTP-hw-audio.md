---
title: Microsoft 蓝牙测试平台-支持音频的外设无线电
description: 蓝牙测试平台 (BTP) 支持的硬件 (音频) 。
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7c636240686ebd92f8af03e54002df7839624677
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803433"
---
# <a name="audio-capable-peripheral-radios"></a>支持音频的外设无线收发器

蓝牙测试平台 (BTP) Traduci 板要求使用12针连接器与任何收音机模块通信。 此处列出的音频无线电和取得突破采用收音机模块，并将所需的 pin 分解为所需的12针布局。

| 单选 | 功能 | 参数 |
| --- | --- | --- |
| RN52 |  (BR) 收音机的基本速率 | rn52 (ex RunPairingTests.bat rn52)  |
| BM64 | 双模式收音机 | bm64 (ex RunPairingTests.bat bm64)  |

## <a name="audio-sled-rn52-radio"></a>音频滑板 (RN52 收音机) 

RN52 是一种基本速率 (BR) ，它可作为音频外设（如扬声器或耳机) ）的浮动网络。 目前计划在即将推出的 BTP 音频测试中支持。 可以通过 [**微芯片**](https://www.microchip.com/wwwproducts/en/RN52)中的 RN52 页找到详细信息。 此滑板打破了无线电的音频输出数据，并将其路由到 Traduci 上的音频编解码器和音频处理 FPGA，以帮助验证。

### <a name="rn52-radio"></a>RN52 广播

![RN52 收音机的照片](images/RN52.png)

### <a name="rn52-radio-on-btp-compatible-sled"></a>BTP 兼容的滑板上的 RN52 收音机

![滑板上 RN52 收音机的照片](images/Traduci_and_RN52.jpg)

> [!NOTE]
> RN52 收音机 **只能** 插入标记为 "JA" 的 Traduci 板12针端口。

- UART 数据连接与 AT 命令用于配置软件
- 支持 SPP、A2DP、HFP 和 AVRCP 配置文件
- 版本3.0 音频模块
- 完全认证类 2 BR 蓝牙 2.1 + EDR
- 小型外形规格，低功率，surface 装模块

## <a name="bm-64-evb-c2-bm64-radio"></a>BM.EXE-64-EVB (BM64 收音机) 

BM64 是一种双模式蓝牙 v 5.0 广播，旨在用于耳机、扬声器或多扬声器外设。
可以通过 [**微芯片**](https://www.microchip.com/wwwproducts/en/BM64)中的 BM64 页找到详细信息。
BM.EXE-64-EVB 允许将 BM64 用作独立设备，从而无需 Traduci 即可连接到测试计算机。
可以通过 [**微芯片**](https://www.microchip.com/DevelopmentTools/ProductDetails/PartNO/BM-64-EVB-C2)中的 bm.exe-64-EVB 页面找到详细信息。

> [!NOTE]
> BM.EXE-64-EVB 开发与类2立体声音频模块版本 (BM.EXE-64-EVB-C2) ，但应与类1音频模块兼容 (BM.EXE 64-EVB-C1) 。

### <a name="bm64-radio"></a>BM64 广播

![BM64 收音机的照片](images/BM64.png)

### <a name="bm64-radio-on-bm64-evaluation-board"></a>BM64 评估板上的 BM64 收音机

![BM.EXE-64-EVB 的照片](images/BM64-EVB-alpha.png)

### <a name="features"></a>功能

- 与自定义数据包结构的 UART 数据连接
- 支持 SPP、A2DP、HFP 和 AVRCP 配置文件
- 蓝牙 v 5。0
- 支持蓝牙双重模式 (BDR/EDR/BLE) 
- 支持 AAC 和 SBC 编解码器
- 大功能的 surface mount 模块
- 使用 BM.EXE-64-EVB 不需要 Traduci
