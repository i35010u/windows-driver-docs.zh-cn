---
title: Microsoft 蓝牙测试平台
description: 支持蓝牙测试平台（BTP）的硬件（HID）。
ms.assetid: a6beeecb-5967-4e08-bfe2-b8aae26861ad
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: f068742df4ef1eb685a4ec73b716bffebc0c2bc7
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528931"
---
# <a name="hid-capable-peripheral-radios"></a>支持 HID 的外设无线收发器 #

蓝牙测试平台（BTP） Traduci 要求使用12针连接器与任何收音机模块通信。 此处列出的 HID 收音机和取得突破采用收音机模块，并将所需的 pin 分解为12针布局。

| 广播 | 功能 | 参数 |
| --- | --- | --- |
| RN42 | 基本速率（BR）广播 | rn42 （例如 RunPairingTests rn42） |
| Bluefruit | 低能耗（LE）广播 | bluefruit （例如 RunPairingTests bluefruit） |

## <a name="pmod-bt2-rn42-radio"></a>PMOD BT2 （RN42 单选钮） ##

RN42 是来自漫游网络的基本费率（BR），可以表现为诸如键盘或鼠标之类的 HID 外围网络。 它当前受 BTP 配对和 HID 测试支持。 有关详细信息，请参阅[Digilent](https://store.digilentinc.com/pmod-bt2-bluetooth-interface/)和[**微芯片**](https://www.microchip.com/wwwproducts/en/RN42)RN42 参考。

可以通过[Digilent](https://store.digilentinc.com/pmod-bt2-bluetooth-interface/)购买 Pmod BT2 收音机

### <a name="rn42-radio"></a>RN42 广播 ###

![RN42 收音机的照片](images/RN42.png)

### <a name="bluetooth-test-platform-traduci-board-and-diligent-sled"></a>蓝牙测试平台 Traduci 板和用心滑板 ###

![Digilent 滑板上的 RN42 收音机照片](images/Traduci_and_DigilentRN42.jpg)

> [!NOTE]
> RN42 收音机**只能**插入标记为 "作业" 的蓝牙测试平台 Traduci 面板端口。

- UART 数据连接
- 支持 HID 配置文件和蓝牙数据链接
- 完全认证类 2 BR 蓝牙 2.1 +
- 小型外形规格，低功率，surface 装模块

## <a name="bluefruit-le-uart-friend-nrf51-radio"></a>Bluefruit LE UART Friend （nRF51 收音机） ##

NRF51 是一种可从北欧半导体（如键盘或鼠标）表现出其他东西的小型能量（LE）广播。 它当前受 BTP 配对和 HID 测试支持。 有关详细信息，请参阅[Adafruit](https://www.adafruit.com/product/2479)和[北欧](https://www.nordicsemi.com/Products/Low-power-short-range-wireless/nRF51822)nRF51822 引用。

可以通过[Adafruit](https://www.adafruit.com/product/2479)购买 BLUEFRUIT LE UART Friend

> [!NOTE]
> Bluefruit 收音机**只能**插入标记为 "JC" 的蓝牙测试平台 Traduci 面板端口。

- UART 数据连接
- 支持 HID 和其他基于 GATT 的服务
- 完全认证的低能耗蓝牙4.1 收音机
- 可配置的 ATT 数据库
- 小型外形规格，低功率，surface 装模块
