---
title: MITT 中的 GPIO 测试
description: MITT 软件包中包含的 GPIO 测试模块可用于测试以下按钮的音量：向上、向下、向下和旋转锁定。
ms.assetid: D50C371B-4A03-4BDD-8EC2-6E7A4A4DF3C5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38fda273039758bf38b259c1ddc79a6946683983
ms.sourcegitcommit: c766ab74e32eb44795cbbd1a4f352d3a6a9adc14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89389597"
---
# <a name="gpio-tests-in-mitt"></a>MITT 中的 GPIO 测试


**上次更新时间**

-   2015年1月

**适用于：**

-   Windows 8.1

MITT 软件包中包含的 GPIO 测试模块可用于测试以下按钮的音量：向上、向下、向下和旋转锁定。 你可以使用这些测试来检测 GPIO 驱动程序和微控制器的问题，并确定系统是响应短推送还是长推送。 MITT 板以物理方式将附加到按钮的行拉低。

## <a name="before-you-begin"></a>开始之前 .。。


-   获取 MITT 板和 GPIO 适配器板。 请参阅 [购买使用 MITT 的硬件](./multi-interface-test-tool--mitt--.md)。
-   [下载 MITT](/previous-versions/dn919810(v=vs.85))软件包。 在受测系统上安装它。
-   在 MITT 板上安装 MITT 固件。 请参阅 [MITT 入门](./get-started-with-mitt---.md)。

## <a name="hardware-setup"></a>硬件设置


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
<th>固定</th>
<th>ACPI 和示意图</th>
<th>连接解决方案</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>GPIO 按钮</td>
<td>按钮和指示器行：音量增加/降低、电源、旋转锁定、笔记本电脑/石板指示器、坞指示器</td>
<td>示意图</td>
<td>调试板上 (简单的男块) </td>
</tr>
<tr class="even">
<td>GPIO 控制器</td>
<td>GPIO 控制器引出线和使用的索引</td>
<td><ul>
<li>用于引线的 GPIO 控制器的 ACPI 名称。</li>
<li>控制器 (级别或基于边缘的) 中的中断触发类型</li>
<li>描述 (包括设备的 PNP ID) ) 如果在测试过程中使用 GPIO pin 来禁用该设备，则 (</li>
</ul></td>
<td>调试板上 (简单的男块) </td>
</tr>
</tbody>
</table>

 

1.  在 MITT 板上，标识 GPIO 连接器。 它使用标签为 " **JA1**" 的最左侧12针标头，如图所示。

    ![mitt 板上的 gpio 标头](images/gpioheader.jpg)

2.  将 GPIO 适配器板连接到 **JA1** 标头。
3.  将 MITT 上的电源跳线连接到3V3。
4.  在 GPIO 标头旁边的开关上向上推送滑块，以打开板的电源。

    ![gpio 电源连接](images/gpiopower.png)

5.   (volu) ，将音量向上，按下音量 (vold) ，将的停放/脱开 (dock) ，并将计算机上的计算机 (模式，) 从安装的操作系统适配器板 (连接到 MITT) 到所测试系统上的相应针脚。

    12针标头连接到各个 GPIO 线路，如图所示。

    ![ja1 标头上的 gpio 布线](images/gpiowiring.png)

    GPIO 板上的输出插针示意图。 Pin 必须与开关并行放置，以便 FET 可以将行的电量降低，就像开关被推送一样。

    ![mitt 上的 gpio 输出插针](images/gpiooutputpin.png)

6.  可选。 如果要对卷或指示器运行 MITT GPIO 测试，但不能同时运行这两个测试，则可以通过设置这些注册表项在 GPIO 自动化中跳过相关测试。 每个条目均为 DWORD，值为1时启用测试;0禁用该方法。
    -   Volume

        **HKEY \_ CURRENT \_ USER \\ Software \\ Microsoft \\ MITT \\ GPIO \\ RunVolumeTest**

    -   指示灯

        **HKEY \_ CURRENT \_ USER \\ Software \\ Microsoft \\ MITT \\ GPIO \\ RunIndicatorsTest**

## <a name="run-gpio-automation-tests"></a>运行 GPIO 自动化测试


若要使用 WDTF 手动运行 GPIO 测试，请执行以下任务：

1.  将 mittsimpleioaction.dll 从 MITT 软件包复制到% ProgramFiles (x86) % \\ Windows 工具包 \\ 8.1 \\ 测试 \\ 运行 \\ 时 WDTF \\ 运行时 \\ 操作 \\ SimpleIO
2.  运行 **% ProgramFiles (x86) % \\ Windows 工具包 \\ 8.1 \\ 测试 \\ 运行 \\ \\ 时 WDTF 运行时 \\UnRegisterWDTF.exe**。
3.  运行 **% ProgramFiles (x86) % \\ Windows 工具包 \\ 8.1 \\ 测试 \\ 运行 \\ \\ 时 WDTF 运行时 \\ 操作 ... \\RegisterWDTF.exe/nogacinstall**
4.  通过运行 \_ \_ \_ MITT 软件包中包含的 SimpleIO MITT gpio SAMPLE 来启动 GPIO 自动化测试。

## <a name="example-custom-gpio-input-injection"></a>示例：自定义 GPIO 输入注入


此示例使用文件 Example.txt，其中包含两秒钟内按下电源按钮的顺序，然后松开按钮。 下面是该文件的内容：

``` syntax
‘h001E8480
‘b0000000000011111
‘b0000000100011111
‘b0000000000011111
```

运行以下命令：

**Muttutil.exe SetChannel 00**

**Muttutil.exe WriteData 0000**

**Muttutill.exe – SetChannel 01**

**Muttutil.exe-WriteDataFromFile Example.txt**

**Muttutil.exe – SetChannel 00**

**Muttutil.exe – Writedata 0001**

-   **SetChannel** with 00 表示控制通道将接收数据。
-   **WriteData** 和0000将暂停所有测试模块。
-   **SetChannel** 选项，方法是指定01，指示 GPIO 通道将接收数据。
-   **WriteDataFromFile** ，其中包含要将示例输入文件的内容发送到 GPIO 模块的文件的名称。
-   **SetChannel** 与00一起切换回控制通道将接收数据。
-   将**WriteData**与0001一起用于激活 GPIO sequencer 的控制通道。 GPIO 模块将开始序列化。

## <a name="generate-input-sequences"></a>生成输入序列


若要生成序列，需要以下值：

-   间隔值

    间隔值是一个位掩码，用于指示在间隔期间按下的按钮。 位掩码中的零值表示在时间间隔内未按下该按钮。 下面是可能的值位索引值：

    | 16位值中的位索引 | 正在测试的系统上的使用情况                      |
    |---------------------------|-----------------------------------------------------|
    | 0                         | 启用电源按钮 ( "1" 启用输出)         |
    | 1                         | 定位指示器启用 ( "1" 启用输出)       |
    | 2                         | 启用启用容量 ( "1" 可启用输出)            |
    | 3                         | 旋转锁定启用 ( "1" 启用输出)        |
    | 4                         | 关闭卷启用 ( "1" 启用输出)          |
    | 5                         | 使用平板电脑切换开关 ( "1" 可启用输出)  |
    | 6-7                       | 未使用                                            |
    | 8                         | 电源按钮值 ( "1" 按开关)          |
    | 9                         | 停靠指示器值 ( "1" 按开关)        |
    | 10                        | 向上 ( "1" 的卷值按开关)             |
    | 11                        | 旋转锁值 ( "1" 按开关)         |
    | 12                        | 按下音量 ( "1" 按开关)           |
    | 13                        | 石板/便携式计算机切换值 ( "1" 按开关)   |
    | 14-15                     | 未使用                                            |

     

-   时钟乘数

    在移动到下一个数据模式之前，时钟乘数是每个数据模式) 为每个数据模式 (的按钮的保持时间。 如果重置线路，GPIO 测试模块将保留最后的数据模式。

    使用较小的和较大的时钟乘数会产生折衷。 乘数的较小值允许更高的精度，这要求您在数据模式中创建更多的行以涵盖 timespan。 你将需要在创建数据模式文件时，确定所需的数据数据包和时钟乘数值之间的适当平衡。

    通过使用前面的示例，您可以创建输入注入文件。 若要生成输入序列，需要通信协议。 从 MITT 板发送到受测系统的数据按以下模式排列：

    ![gpio 模块的通信协议](images/gpioprotocol.png)

    GPIO 测试线路中没有协议级别的错误检查。 如果出现协议错误，MITT 将显示未知错误。

## <a name="gpio-adapter-schematic"></a>GPIO 适配器示意图


![gpio 示意图](images/gpioschematic.png)

## <a name="related-topics"></a>相关主题
[通过多接口测试工具进行测试 (MITT) ](./testing-with-multi-interface-test-tool--mitt-.md)