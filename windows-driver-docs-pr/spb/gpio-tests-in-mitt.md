---
title: MITT 中的 GPIO 测试
description: MITT 软件程序包中包含的 GPIO 测试模块可用于测试以下按钮卷会关闭电源，以及旋转锁的卷。
ms.assetid: D50C371B-4A03-4BDD-8EC2-6E7A4A4DF3C5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b0bc3c5ac0c6a2687c096a9edf5f6423a69bfd9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373775"
---
# <a name="gpio-tests-in-mitt"></a>MITT 中的 GPIO 测试


**上次更新时间**

-   2015 年 1 月

**适用于：**

-   Windows 8.1

MITT 软件程序包中包含的 GPIO 测试模块可用于测试以下按钮卷会关闭电源，以及旋转锁的卷。 可以使用这些测试要检测的 GPIO 驱动程序和微控制器的问题和确定对短期或长期推送的系统响应是否为所需的响应。 附加到按钮的行以物理方式由 MITT 委员会拉取低。

## <a name="before-you-begin"></a>开始之前...


-   获取 MITT 板和 GPIO 适配器板。 请参阅[购买硬件使用 MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/multi-interface-test-tool--mitt--)。
-   [下载 MITT 软件包](https://docs.microsoft.com/previous-versions/dn919810(v=vs.85))。 待测试系统上安装它。
-   安装 MITT 固件 MITT 板上。 请参阅[开始使用 MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/get-started-with-mitt---)。

## <a name="hardware-setup"></a>硬件安装


![mitt gpio 硬件安装](images/mitttogpio.jpg)

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>总线接口</th>
<th>引出线</th>
<th>ACPI 和图表</th>
<th>连接解决方案</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>GPIO 按钮</td>
<td>按钮和指示符的代码行：卷向上/向下，电源、 旋转锁、 便携式计算机/盖板指示器、 停靠指示器</td>
<td>图表</td>
<td>（在调试开发板） 的简单男性块</td>
</tr>
<tr class="even">
<td>GPIO 控制器</td>
<td>GPIO 控制器引出线和使用索引</td>
<td><ul>
<li>ACPI 的用于引出线的 GPIO 控制器的名称。</li>
<li>中断控制器 （级别或基于 edge） 中的触发类型</li>
<li>使用 GPIO 固定到测试传递过程中禁用的设备 （如果有） 的说明 （包括其即插即用 ID）</li>
</ul></td>
<td>（在调试开发板） 的简单男性块</td>
</tr>
</tbody>
</table>

 

1.  MITT 板上标识 GPIO 连接器。 它使用 left 最 12 pin 标头，标有**JA1**，此图中所示。

    ![gpio mitt 板上的标头](images/gpioheader.jpg)

2.  连接到的 GPIO 适配器看板**JA1**标头。
3.  连接到 3V3 MITT 板上的电源跳线。
4.  将滑块推送上要为开发板供电的 GPIO 标头旁边的开关。

    ![gpio power 连接](images/gpiopower.png)

5.  音量增大 (volu)、 (vold) 减小音量、 停靠/取消停靠 （停靠） 和盖板/便携式计算机 （模式） 行从 GPIO 适配器看板 （连接到 MITT） 连接到待测试系统上的相应针。

    此图中所示，12 pin 标头被绑定到 GPIO 的各个行。

    ![gpio 接线上 ja1 标头](images/gpiowiring.png)

    输出插针 GPIO 板上的示意图。 Pin 必须位于与交换机并行以便 FET 可以提取行低，像按开关。

    ![gpio 输出插针上 mitt](images/gpiooutputpin.png)

6.  可选。 如果你想要在卷或指示器，但不是能同时运行 MITT GPIO 测试，您可以通过设置这些注册表项中跳过 GPIO 自动化中的相关的测试。 每个条目是一个 dword 值，它的值为 1 使测试;0 禁用它。
    -   Volume

        **HKEY\_CURRENT\_USER\\Software\\Microsoft\\MITT\\GPIO\\RunVolumeTest**

    -   指示器

        **HKEY\_CURRENT\_USER\\Software\\Microsoft\\MITT\\GPIO\\RunIndicatorsTest**

## <a name="run-gpio-automation-tests"></a>运行 GPIO 自动化测试


若要使用 WDTF GPIO 测试运行手动，请执行以下任务：

1.  将 mittsimpleioaction.dll 从 MITT 软件程序包复制到 %programfiles （x86） %\\Windows 工具包\\8.1\\测试\\运行时\\WDTF\\运行时\\操作\\SimpleIO
2.  运行 **%programfiles （x86） %\\Windows 工具包\\8.1\\测试\\运行时\\WDTF\\运行时\\UnRegisterWDTF.exe**。
3.  Run **%ProgramFiles(x86)%\\Windows Kits\\8.1\\Testing\\Runtimes\\WDTF\\RunTime\\Actions ..\\RegisterWDTF.exe /nogacinstall**
4.  首先 GPIO 自动化测试运行 SimpleIO\_MITT\_ GPIO \_Sample.vbs 纳入 MITT 软件程序包。

## <a name="example-custom-gpio-input-injection"></a>例如：自定义 GPIO 输入注入


此示例使用一个文件，Example.txt，包含两秒钟按电源按钮，然后释放按钮的序列。 下面是该文件的内容：

``` syntax
‘h001E8480
‘b0000000000011111
‘b0000000100011111
‘b0000000000011111
```

运行以下命令：

**Muttutil.exe -SetChannel 00**

**Muttutil.exe -WriteData 0000**

**Muttutill.exe –SetChannel 01**

**Muttutil.exe – WriteDataFromFile Example.txt**

**Muttutil.exe –SetChannel 00**

**Muttutil.exe –Writedata 0001**

-   **SetChannel** 00 指示控制通道将接收数据。
-   **WriteData** 0000 暂停所有测试模块。
-   **SetChannel**通过指定 01 的选项以指示 GPIO 通道将接收数据。
-   **WriteDataFromFile**要发送到 GPIO 模块的示例输入文件的内容文件的名称。
-   **SetChannel**通道将与 00，切换回该控件接收数据。
-   **WriteData**与 0001 到要激活 GPIO sequencer 的控制通道。 GPIO 模块将进行序列化。

## <a name="generate-input-sequences"></a>生成输入的序列


若要生成的序列，需要这些值：

-   间隔值

    间隔值是一个位掩码，指示在间隔期间按下的按钮。 位掩码中的零值指示的时间间隔内未按下按钮。 以下是可能的值比索引值：

    | 16 位值中的位索引 | 待测试系统上的使用情况                      |
    |---------------------------|-----------------------------------------------------|
    | 0                         | 电源按钮启用 （"1"启用输出）        |
    | 1                         | 停靠指示器启用 （"1"启用输出）      |
    | 2                         | 启用增大音量 （"1"启用输出）           |
    | 3                         | 旋转锁启用 （"1"启用输出）       |
    | 4                         | 启用减小音量 （"1"启用输出）         |
    | 5                         | 静态图像/便携式计算机上切换启用 （"1"启用输出） |
    | 6-7                       | 不使用                                            |
    | 8                         | 电源按钮的值 （"1"按交换机）         |
    | 9                         | 停靠指示器值 （"1"按交换机）       |
    | 10                        | 音量增大值 （"1"按交换机）            |
    | 11                        | 旋转锁值 （"1"按交换机）        |
    | 12                        | 增大音量值 （"1"按交换机）          |
    | 13                        | 静态图像/便携式计算机上切换值 （"1"按交换机）  |
    | 14-15                     | 不使用                                            |

     

-   时钟乘数

    时钟乘数移到下一步的数据模式之前是为每个数据模式的持续时间 （以一个低至微秒为增量） 的按钮。 GPIO 测试模块保存数据的最后一个模式，直到重置该线路。

    没有使用与大型时钟乘数的较小的权衡。 较小值为乘数允许更高的精度，这要求在数据模式覆盖一个 timespan，用于创建更多的行。 您需要决定所需的数据包和时钟乘数值之间的适当平衡时创建的数据模式文件。

    通过使用前面的示例中可以创建输入的注入文件。 若要生成的输入的序列，您需要的通信协议。 从 MITT 板发送到待测试系统的数据被排列在此模式：

    ![gpio 模块的通信协议](images/gpioprotocol.png)

    没有签入 GPIO 测试线路协议级别错误。 如果协议错误，MITT 显示出现未知的错误。

## <a name="gpio-adapter-schematic"></a>GPIO 适配器示意图


![gpio 示意图](images/gpioschematic.png)

## <a name="related-topics"></a>相关主题
[使用多接口测试工具 (MITT) 进行测试](https://docs.microsoft.com/windows-hardware/drivers/spb/testing-with-multi-interface-test-tool--mitt-)  



