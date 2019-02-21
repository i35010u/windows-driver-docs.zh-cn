---
title: 在 MITT 电容式触摸测试
description: MITT 软件程序包中的电容式触摸测试需要 MCATT （Microsoft 电容式应用程序测试工具）。
ms.assetid: 86E4D489-7DC3-4765-85BE-3706B3CA6C0B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e98f80fa90859a2ca62803a0611608c4d0d95c2e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519266"
---
# <a name="capacitive-touch-tests-in-mitt"></a>在 MITT 电容式触摸测试


**上次更新时间**

-   2015 年 1 月

**适用于：**

-   Windows 8.1

MITT 软件程序包中的电容式触摸测试需要 MCATT （Microsoft 电容式应用程序测试工具）。 它是用于验证基于电容式触控硬件 （触摸板和触摸屏） 自动化工具。 MCATT 包括了用于编程 MCATT 设备和自动的测试的简单接口。 可以使用测试来检测虚影点或确定第一个触摸屏输入传播后系统唤醒时间表。

您可以使用这些测试用例 MCATT:

-   压力测试
-   目标的延迟度量
-   如在板上执行输入时的电源转换 SimpleIo/设备基础方案。

## <a name="before-you-begin"></a>开始之前...


-   获取 MITT 看板。 请参阅[购买硬件使用 MITT](https://msdn.microsoft.com/library/windows/hardware/dn919811)。
-   获取触摸模拟器板和带外电缆连接到适配器。
-   获取有 40 pin 适配器以 MITT 板连接到触摸模拟器板 MCATT 扩展板。
-   [下载 MITT 软件包](https://msdn.microsoft.com/library/windows/hardware/dn919810)。
-   安装 MITT 固件 MITT 板上。 请参阅[开始使用 MITT](https://msdn.microsoft.com/library/windows/hardware/dn919779)。

## <a name="hardware-setup"></a>硬件安装


![mcatt 安装程序](images/mcatt-hardware-setup.png)

1.  连接到 40 pin 适配器 MITT 板。
2.  触摸模拟器板连接到适配器。
3.  使用 USB 电缆，将其连接到主计算机 MITT 板。
4.  使用 USB 电缆连接到主机系统的待测试系统。 这可以是一个 A USB 电缆或从待测试系统的完全连接到待测试设备以有线方式。

    ![mcatt 连接](images/mcatt-setup.png)

## <a name="mcatt-manual-tests"></a>MCATT 手动测试


若要手动运行 MCATT 测试，请执行以下任务：

1.  将复制到 mittsimpleioaction.dll:\[WDTF 目录\]\\操作\\SimpleIO
2.  运行\[WDTF 目录\]\\UnRegisterWDTF.exe
3.  运行\[WDTF 目录\]\\RegisterWDTF.exe

## <a name="example-sending-input-sequence"></a>示例：发送输入的序列


可以通过编程看板，在循环中运行指定的接触点序列。

在任何给定时间的触摸点的脚本控件提供模拟。 该脚本可以描述请逐个框架的接触点来模拟用户笔势，例如点击，pan （慢速拖动） 或笔锋 (加速 pan) 集。

下面是示例，用于生成测试模块中包含一个简单的平移手势。 此示例测试适用于具有此编号约定的 5 x 8 看板。

![mcatt 模式](images/mcatt-pattern.png)

运行以下命令：

**Muttutil.exe -SetChannel 00**

**Muttutil.exe -WriteData 0000**

**Muttutill.exe –SetChannel 02**

**Muttutil.exe – WriteDataFromFile Example.txt**

**Muttutil.exe –SetChannel 00**

**Muttutil.exe –Writedata 0004**

-   **SetChannel** 00 指示控制通道将接收数据。
-   **WriteData** 0000 暂停所有测试模块。
-   **SetChannel**选项通过指定 02 选择 MCATT 模块。
-   **WriteDataFromFile**要发送到 MCATT 模块的示例输入文件的内容文件的名称。
-   **SetChannel**通道将与 00，切换回该控件接收数据。
-   **Writedata** 0004 MCATT 序列运行文件中使用。 如果你想要循环的序列，而不是 0004 使用 000 C。

以下是示例模式：

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

在前面的示例中，第一行设置到 0x00028480，模式速率或每行 164,992 微秒为单位。 其余行用于指示已连接到地面板和浮动的面板。 有 40 面板，因此每一行都是 40 位长时间使用位 39 左侧和右侧的行和第 0 位行右侧。 此模式以通过按下上填充 26、 27、 38 和 39，通过设置这些位为"1"，然后将按从看板的左侧移到的看板的创建模式使用示例模式作为起始点的权限。 可以创建并使用编辑 MCATT 模式文件[MCATT 模式编辑器](https://msdn.microsoft.com/library/windows/hardware/dn919809)。

## <a name="related-topics"></a>相关主题
[使用多接口测试工具 (MITT) 进行测试](https://msdn.microsoft.com/library/windows/hardware/dn919874)  



