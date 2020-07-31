---
title: Microsoft 蓝牙测试平台支持的硬件
description: 支持蓝牙测试平台（BTP）的硬件。
ms.assetid: a6beeecb-5967-4e08-bfe2-b8aae26861ad
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: ed8c7f2740469a236330f4cff5bf090a0fff72d5
ms.sourcegitcommit: 7a7ce6070ed16673108cc64c33b3ddb894453cfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87412532"
---
# <a name="bluetooth-testing-platform-supported-hardware"></a>支持蓝牙测试平台的硬件

蓝牙测试平台（BTP）利用专用硬件使蓝牙测试更容易。 Traduci 板用于更轻松地允许主机设备（如 PC）上的软件与 sideband 上的外部无线电设备通信。

例如，LE 配对测试需要启用外围广播，具有某些 IO 功能，并在其配对之前播发为可连接/可发现。 外围广播具有定义完善的命令，因此，主机上的 BTP 软件会将这些命令通过 USB 发送到 Traduci，后者又将其路由到相应的广播。 成功完成这些命令后，BTP 软件会通过向外设无线电请求主机对来继续测试，现已准备好接受配对。

在上面的方案中，Traduci 提供了几个更简单的功能：可以使用无线收发器的正确电压提供和切断电源，还可以将不同的命令路由到不同的无线电收发器，并通过正确的协议和波特率来调解此通信。

此外，请务必注意，BTP 测试不具有对 Traduci 的紧密依赖关系。 如果测试需要其他外部硬件，则 BTP 旨在允许轻松扩展以支持该方案。

## <a name="traduci-board"></a>Traduci 板
Traduci 板由[MCCI](https://mcci.com/usb/dev-tools/model-2411/)提供

![Traduci 板的照片](images/Traduci_Overhead.jpg)

- 4 12-pin 端口，可同时支持4个收音机
- 能够同时向多个无线电收发数据
- 3个 Fpga 分别连接到端口1、2和3
- 通过集成音频编解码器支持音频测试
- 根据插入端口的无线电需要，可以轻松地将 Unlabled pin 静态分配到高或低
- Traduci 目前不支持使用 CTS 和 RTS 进行硬件握手

## <a name="supported-radios"></a>支持的无线电

目前，仅正式支持 RN42 （BR）和 Bluefruit （LE）无线电收发器。 它们都可以运行配对和 HID 测试。 有关这些无线电收发器的详细信息，可以 reviwed 在[支持 HID 功能的外围无线电设备](testing-BTP-hw-hid.md)上。

正在开发音频测试。 有关将使用的音频收音机的详细信息，请参阅[支持音频的外设无线电收发](testing-BTP-hw-audio.md)器。