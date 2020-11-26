---
title: MITT 中的电容式触控测试
description: MITT 软件包中的电容式触控测试需要 MCATT (Microsoft 电容式应用程序测试工具) 。
ms.assetid: 86E4D489-7DC3-4765-85BE-3706B3CA6C0B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83e34faa0f1e77e67415840fccaced8596192bb4
ms.sourcegitcommit: 0c3cab853b0b75149b7604eef03275f997792a84
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2020
ms.locfileid: "96157263"
---
# <a name="capacitive-touch-tests-in-mitt"></a>MITT 中的电容式触控测试

MITT 软件包中的电容式触控测试需要 MCATT (Microsoft 电容式应用程序测试工具) 。 它是一个自动化工具，用于验证基于电容式的触摸硬件 (触摸板和 touchscreens) 。 MCATT 包含一个用于对 MCATT 设备进行编程和自动测试的简单接口。 你可以使用这些测试来检测虚影点，或确定第一个触摸输入在系统唤醒后传播的时间表。

对于这些测试用例，可以使用 MCATT：

- 压力测试
- 目标延迟度量
- SimpleIo/设备基础方案，例如在 pad 上执行输入时的电源转换。

## <a name="before-you-begin"></a>开始之前

- 获取 MITT 板。 请参阅 [购买使用 MITT 的硬件](./multi-interface-test-tool--mitt--.md)。
- 获取触控模拟器板和带缆线连接到适配器。
- 获取一个 MCATT 扩展板，其中包含40针适配器，以将 MITT 板连接到触控模拟器板。
- [下载 MITT](/previous-versions/dn919810(v=vs.85))软件包。
- 在 MITT 板上安装 MITT 固件。 请参阅 [MITT 入门](./get-started-with-mitt---.md)。

## <a name="hardware-setup"></a>硬件设置

![mcatt 安装程序](images/mcatt-hardware-setup.png)

1. 将 MITT 板连接到40针适配器。
2. 将触摸模拟器 pad 连接到适配器。
3. 使用 USB 电缆将 MITT 板连接到主计算机。
4. 使用 USB 电缆将正在测试的系统连接到主机系统。 这可以是一种从 A 到 A 的 USB 电缆，也可以是一条连接在受测系统与受测设备之间的连接。

    ![mcatt 连接](images/mcatt-setup.png)

## <a name="mcatt-manual-tests"></a>MCATT 手动测试

若要手动运行 MCATT 测试，请执行以下任务：

1. 将 mittsimpleioaction.dll 复制到： \[ WDTF directory \] \\ Actions \\ SimpleIO
2. 运行 \[ WDTF 目录 \] \\UnRegisterWDTF.exe
3. 运行 \[ WDTF 目录 \] \\RegisterWDTF.exe

## <a name="example-sending-input-sequence"></a>示例：发送输入序列

可以将此板编程为在循环中运行指定的触摸点序列。

在任意给定时间，该脚本控制哪些触点提供模拟。 此脚本可以逐个描述一组触摸点，以模拟用户手势（如点击、平移 (缓慢拖动) 或笔锋 (加速平移) 。

下面是一个示例，用于生成包含在测试模块中的简单平移手势。 此示例测试适用于具有此编号约定的5x8 板。

![mcatt 模式](images/mcatt-pattern.png)

运行以下命令：

`Muttutil.exe -SetChannel 00`

`Muttutil.exe -WriteData 0000`

`Muttutill.exe –SetChannel 02`

`Muttutil.exe –WriteDataFromFile Example.txt`

`Muttutil.exe –SetChannel 00`

`Muttutil.exe –Writedata 0004`

- **SetChannel** with 00 表示控制通道将接收数据。
- **WriteData** 和0000将暂停所有测试模块。
- **SetChannel** 选项，方法是指定02以选择 MCATT 模块。
- **WriteDataFromFile** ，其中包含要将示例输入文件的内容发送到 MCATT 模块的文件的名称。
- **SetChannel** 与00一起切换回控制通道将接收数据。
- **Writedata** with 0.0004 在文件中运行 MCATT 序列。 如果希望序列循环，请使用000C 而不是0.0004。

下面是示例模式：

``` syntax
'h00028480
'b1100000000001100000000000000000000000000
'b1000000000001000000000000000000000000000
'b1000000000011010000000000000000000000000
'b0000000000010010000000000000000000000000
'b0000000000010010000011000000000000000000
'b0000000000000000000011000000000000000000
'b0000000000000000000011000000000000010001
'b0000000000000000000000000000000000010001
'b0000000000000000000000000000000000110011
'b0000000000000000000000000000000000100010
'b0000000000000000000000000000000001100110
'b0000000000000000000000000000000001000100
'b0000000000000000000000000000000011001100
'b0000000000000000000000000000000010001000
'b0000000000000000000000000000000000000000
'b0000000000000000000000000000000000000000
```

在前面的示例中，第一行将模式速率设置为0x00028480，或每行164992微秒。 其余行用于指示连接到地面的垫和浮动的垫。 有40的 pad，因此每行的长度为40位，行的左侧有位39，位0位于行右侧。 此模式通过以下方式开始：按 39 38 下，将这些位设置为 "1"，然后从棋盘的左侧向右移动，以创建模式，使用该示例模式作为起始点即可。 可以通过使用 [MCATT 模式编辑器](/previous-versions/dn919809(v=vs.85))来创建和编辑 MCATT 模式文件。
