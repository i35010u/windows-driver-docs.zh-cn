---
title: Microsoft 蓝牙测试平台-支持 HID 的外设无线电
description: 适用于支持的硬件 (HID) 的蓝牙测试平台 (BTP) 。
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1787ef0dad77a6387f0a2a7c8e11dd49636d147c
ms.sourcegitcommit: 7b3bddc91b87de5afce36c120620497c37234fbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98812004"
---
# <a name="hid-capable-peripheral-radios"></a>支持 HID 的外设无线收发器

蓝牙测试平台 (BTP) Traduci 要求使用12针连接器与任何收音机模块通信。 此处列出的 HID 收音机和取得突破采用收音机模块，并将所需的 pin 分解为12针布局。

| 单选 | 功能 | 参数 |
| --- | --- | --- |
| RN42 |  (BR) 收音机的基本速率 | rn42 (ex RunPairingTests.bat rn42)  |
| Bluefruit | 低能耗 (LE) 收音机 | bluefruit (ex RunPairingTests.bat bluefruit)  |

## <a name="pmod-bt2-rn42-radio"></a>PMOD BT2 (RN42 收音机) 

RN42 是的一种基本速率 (BR) 的广播网络，可以表现为诸如键盘或鼠标等 HID 外围网络。 它当前受 BTP 配对和 HID 测试支持。 有关详细信息，请参阅 [Digilent](https://store.digilentinc.com/pmod-bt2-bluetooth-interface/) 和 [**微芯片**](https://www.microchip.com/wwwproducts/en/RN42) RN42 参考。

可以通过[Digilent](https://store.digilentinc.com/pmod-bt2-bluetooth-interface/)购买 Pmod BT2 收音机

### <a name="rn42-radio"></a>RN42 广播

![RN42 收音机的照片](images/RN42.png)

### <a name="bluetooth-test-platform-traduci-board-and-diligent-sled"></a>蓝牙测试平台 Traduci 板和用心滑板

![Digilent 滑板上的 RN42 收音机照片](images/Traduci_and_DigilentRN42.jpg)

> [!NOTE]
> RN42 收音机 **只能** 插入标记为 "作业" 的蓝牙测试平台 Traduci 面板端口。

- UART 数据连接
- 支持 HID 配置文件和蓝牙数据链接
- 完全认证类 2 BR 蓝牙 2.1 +
- 小型外形规格，低功率，surface 装模块

## <a name="bluefruit-le-uart-friend-nrf51-radio"></a>Bluefruit LE UART Friend (nRF51 收音机) 

NRF51 是一种低能耗 (LE) 从北欧的半导体收音机，可以表现为 HID 外围设备 (如键盘或鼠标) 其他东西。 它当前受 BTP 配对和 HID 测试支持。 有关详细信息，请参阅 [Adafruit](https://www.adafruit.com/product/2479) 和 [北欧半导体](https://www.nordicsemi.com/Products/Low-power-short-range-wireless/nRF51822) nRF51822 参考。

可以通过[Adafruit](https://www.adafruit.com/product/2479)购买 BLUEFRUIT LE UART Friend

> [!NOTE]
> Bluefruit 收音机 **只能** 插入标记为 "JC" 的蓝牙测试平台 Traduci 面板端口。

- UART 数据连接
- 支持 HID 和其他基于 GATT 的服务
- 完全认证的低能耗蓝牙4.1 收音机
- 可配置的 ATT 数据库
- 小型外形规格，低功率，surface 装模块
