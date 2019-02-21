---
Description: The MUTT Connection Exerciser Type-C (USB Type-C ConnEx) hardware board is a custom shield for the Arduino board.
title: 测试与 USB 类型 C ConnEx USB C 类型系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1bd672f37af43f807d9b178112bef18671d4fc2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544860"
---
# <a name="test-usb-type-c-systems-with-usb-type-c-connex"></a>测试与 USB 类型 C ConnEx USB C 类型系统


**摘要**

-   自动测试通过使用 USB 类型 C ConnEx
-   在 Windows 10 USB 类型 C 互操作性测试过程： 功能测试 (FT) 和压力测试 (ST)。
-   诊断过程和提示以确认方案，例如设备添加和删除。

**适用于**

-   Windows 10

**正式规范和过程**

-   [USB 3.1 和 USB 类型 C 规范]( https://go.microsoft.com/fwlink/p/?LinkId=620208)
-   [xHCI 互操作性测试过程](https://go.microsoft.com/fwlink/p/?LinkId=623257)

**上次更新时间**

-   2016 年 2 月

\[有些信息与预发布产品的商业发布之前可能有大幅度修改。 Microsoft 不做任何明示或暗示的担保，此处提供的信息。\]

MUTT 连接试验程序类型-C (USB 类型 C ConnEx) 硬件转插板是 arduino 开发板的自定义防护罩。 防护罩提供四个开关来自动执行 USB 类型 C 方案的互操作性测试。

本主题提供了自动测试系统、 设备、 USB 类型 C 连接器使用停靠和与 Windows 操作系统及其互操作性的指导原则。 你可以测试硬件属于以下类别之一：

-   系统：台式计算机、 便携式计算机、 平板电脑、 服务器或与公开 USB 类型 C 端口运行的 Windows 操作系统版本的 SKU 的手机。
-   停靠：公开多个端口的任何 USB 类型 C 设备。
-   设备：与可以附加到系统或停靠类型 C 端口的任何 USB 设备。 此类别包括传统的 USB 设备以及设备支持 USB 类型 C 规范中定义的附件和备用模式。

## <a name="hardware-requirements"></a>硬件要求


若要使用 USB 类型 C ConnEx 执行 USB 类型 C 互操作性测试过程，需要：

-   **待测系统 (SUT)**

    台式计算机、 便携式计算机、 平板电脑、 服务器或与至少一个公开类型 C USB 端口的电话。

-   **Arduino Mega 2560 R3**

    [Arduino 庞大 2560 R3](https://go.microsoft.com/fwlink/p/?LinkId=733526)用作测试安装微型控制器。 可以从购买此板[Arduino 应用商店](https://go.microsoft.com/fwlink/p/?LinkId=733526)。

    ![arduino 开发](images/arduino.png)

-   **微型控制器的电源适配器**。

    有关兼容适配器为 Arduino 庞大 2560 R3 电路板[请参阅此站点](https://go.microsoft.com/fwlink/p/?LinkID=733660)。

-   **USB 类型 C ConnEx**

    防护罩有一个男性 USB 类型 C 端口 (标有**J1**) 连接到的 SUT 是。 防护罩还具有其他四个 USB 端口 (标有**J2**， **J3**， **J4**， **J6**) 到哪些设备可以是到外围设备作为附加该 actSUT。 防护罩监视电流与电压来自 SUT。 您可以购买此板从[MCCI](https://go.microsoft.com/fwlink/p/?LinkId=733488)或[JJG 技术]( https://go.microsoft.com/fwlink/p/?linkid=618287)。

    ![USB 类型 C ConnEx](images/connexc-top.png)

-   **USB A 到 B 电缆**

    将使用此电缆连接到微型控制器以微控制器运行测试上的固件更新的电脑。

-   **外围 USB 设备**

    可以附加到 SUT 的 USB 类型 C 端口使用任何 USB 设备。 此类别包括传统的 USB 设备和其他设备的支持 USB 类型 C 规范中定义的附件和备用模式。

-   **USB 充电**

    USB 类型 C 支持 USB 类型 C 当前要求和 （可选） [USB 供电](https://go.microsoft.com/fwlink/p/?LinkID=623310)。 您还需要为 USB Micro B 充电器**J6**。

-   **代理控制器**

    USB 类型 C ConnEx 可通过使用代理运行测试的控制。 代理控制器可以为这些实体之一：

    -   辅助台式 PC 或便携式计算机。

        与移动的 SUT; 代理控制器通信若要加载固件微控制器。

    -   通过使用辅助 USB 端口的 SUT。
    -   通过使用 3.5mm 音频插孔 SUT。

        在此设置，您需要：

        -   若要使用单个 USB 类型 C 端口 Sut 上运行测试的 DTMF 防护罩。 DTMF 提供的功能来控制防护罩从单端口设备使用的音频插孔，固件初始立刻正式投入工作完成后。

            ![dtmf 防护罩](images/dtmf.png)

        -   用于连接到 SUT 的 DTMF 防护罩 4 pin 男性男性音频电缆。 这样，以控制着测试期间 USB 类型 C 防护罩 SUT。

            ![3.5mm 音频插孔](images/audio-jack.png)

## <a name="software-requirements"></a>软件要求


请确保满足这些要求：

-   你 SUT 必须有想要测试互操作性的 Windows 操作系统版本。
-   代理控制器必须运行 Windows 10。
-   [![下载 mutt 软件包](images/download.png)](https://go.microsoft.com/fwlink/p/?LinkId=786621)和代理控制器上安装最新的 MUTT 软件包。
-   包是一套用于使用 USB 类型 C ConnEx 运行测试的工具。

    它包括实用程序来更新固件、 切换在外围设备的端口，并发送请求，以模拟测试用例。 它还包含测试的总线、 其控制器和设备连接到该总线功能的测试驱动程序包。

-   测试工具的安装需要提升的命令窗口。

    若要打开提升的命令窗口，用户必须属于**管理员**代理控制器组。 若要打开提升的命令提示符窗口，创建到 Cmd.exe 的桌面快捷方式，右键单击 Cmd.exe 快捷方式，然后选择**以管理员身份运行**。

### <a name="usb-type-c-connex-tools"></a>USB 类型 C ConnEx 工具

以下是特定于 USB 类型 C ConnEx 中 MUTT 软件包的工具

| 工具                          | 描述                                                                                          |
|-------------------------------|------------------------------------------------------------------------------------------------------|
| [ConnExUtil.exe](#connexutil) | 命令行工具来执行 USB 类型 C ConnEx 功能。                                             |
| [CxLoop.cmd](#cxloop)         | 连接和断开连接的每个端口一次。                                                             |
| [CxStress.cmd](#cxstress)     | 随机的压力脚本。                                                                            |
| [CxPower.cmd](#cxpower)       | 一段时间内捕获 power 数据 （电压和电流），并将输出发送到 CSV 文件。 |



有关所有其他工具的信息，请参阅[MUTT 软件包中的工具](mutt-software-package.md)。

## <a name="get-started"></a>获取已启动...


按照以下过程来设置测试环境。

![USB 类型 C ConnEx 配置](images/connexc.png)

配置应类似于此映像。 请注意微型控制器上的 USB 类型 C 端口提供了对 USB 类型 C ConnEx 时连接到电脑的控制。

在这些步骤中，将连接的硬件部分、 微型控制器上的固件更新并验证安装。 DTMF 防护罩提供对 USB 类型 C ConnEx 连接到手机或平板电脑的音频端口时控制。

1.  连接到 USB 类型 C 防护罩微型控制器。

    如果 USB 类型 C ConnEx 而未进入已组装，然后继续步骤 1。 如果你 USB 类型 C ConnEx 经过组装，然后转到步骤 2。

    **谨慎**![警告：](images/caution.png)因为球瓶轻松弯曲必须谨慎地执行此步骤。  



    1.  通过确保委员会为每个其他级别对齐微型控制器上接收器使用的 USB 类型 C 防护的 pin。

        ![对齐 USB 类型 C ConnEx 的 pin](images/connexc-align.png)

    2.  轻轻一起按这两种主板。 要小心不要弄弯防护罩上的球瓶。

        ![组装 USB 类型 C ConnEx](images/connexc-connect.png)

        你已组装的单元应类似于此图像：

        ![连接 connex c 板](images/connexc-connect1.png)

2.  Power USB 类型 C ConnEx 从附加的微型控制器通过使用任一 USB 类型-B （连接到代理控制器） 或从外部电源适配器。 LCD 显示器是类似于此图像：

    在 5 秒后 LCD 屏幕将显示的电流与电压。

    ![USB 类型 C ConnEx 固件启动之前](images/connexc-connect2.png)![USB 类型 C ConnEx 固件启动之前](images/connexc-connect3.png)

    如果这样做不，请参阅显示上一图中所示，请确保你已正确收集了单元。

3.  使用 USB 类型 C ConnEx 固件更新微型控制器。
    -   打开提升的命令提示符窗口。
    -   导航到 MUTT 软件包，如 c： 的位置\\Program Files (x86)\\USBTest\\*&lt;arch&gt;*。
    -   运行以下命令：

        **MuttUtil.exe – UpdateTabFirmware**

4.  插入到男性 USB 类型 C 端口 SUT (标有**J1**) 上防护罩。

    **谨慎** **J1**连接器连接 SUT 时需要其他支持。 连接器不足够稳定，可承受的设备或单独的权重。

    ![附加待测系统 (sut)](images/connexc-connect4.png)

5.  将外围设备连接到标有的 USB 端口**J2**， **J3**， **J4**， **J6**。

    ![将外围设备连接到 USB 类型 C ConnEx](images/connexc-connect7.png)

6.  将代理控制器附加到微型控制器。
    -   如果代理控制器是台式计算机或便携式计算机，请通过 USB 建立连接。 上图中所示，微控制器上的 USB 类型 B 端口连接到代理控制器上的 USB 端口。
    -   如果代理控制器移动 SUT，通过使用音频端口建立连接。 对于此连接，您需要 DTMF 防护罩。
        1.  连接到已组装单元 DTMF 防护罩，此图中所示：

            ![dtmf 附件](images/connexc-connect6.png)

        2.  使用 4 pin 男性男性音频电缆防护罩的音频端口连接到 SUT 上的音频端口。

            你的设置应类似于此图像：

            ![附加待测系统 (sut 与 dtmf)](images/connexc-connect5.png)

7.  请确保 USB 类型 C ConnEx 识别代理控制器上的设备管理器。
    1.  右键单击任务栏中的开始按钮并选择**设备管理器**。
    2.  展开**端口 （COM 和 LPT）** 节点并记下 COM 端口由微型控制器。 在此示例中，它被连接到 COM 4。

        ![USB 设备管理器中的类型 C ConnEx](images/connexc-connect8.png)

## <a name="connexutilexe"></a>ConnExUtil.exe


以下是用于控制 USB 类型 C ConnEx 板 ConnExUtil.exe 支持的命令行选项。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>用例</th>
<th>选项</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>设备发现
<p>列出所有设备连接到 USB 类型 C ConnEx</p></td>
<td><strong>/list</strong></td>
<td>对于连接的 USB 设备，此选项可列出设备实例路径。 显示了对于音频连接的设备<strong>音频</strong>。
<p>若要查看音频设备，请使用以下结合<strong>/all</strong>参数。 使用从 1 开始的索引，它可用于输入列表<strong>/#</strong>参数。</p></td>
</tr>
<tr class="even">
<td>选择设备
<p>选择所有设备连接到 USB 类型 C ConnEx，包括音频。</p></td>
<td><strong>/all</strong></td>
<td>可选。
<p>如果没有此参数的实用程序地址 USB 连接的设备。 使用此参数仅当连接的音频设备正在使用中。 音频发现非常耗时且默认情况下禁用。</p></td>
</tr>
<tr class="odd">
<td>选择设备
<p>选择特定的设备连接到 USB 类型 C ConnEx ' n '。</p></td>
<td><strong>/#</strong> <em>n</em></td>
<td>（可选）
<p>输入<em>n</em>可用设备的基于 1 的索引连接到可通过查看 USB 类型 C ConnEx <strong>/list</strong>参数。 如果没有此参数，默认行为是所有 USB 类型 C ConnEx 板上运行每个命令。</p></td>
</tr>
<tr class="even">
<td>设备命令</td>
<td><strong>/setPort</strong> <em>p</em></td>
<td>切换到指定的端口<em>p</em>。
<p>通过指定数量 (1-4) 或按名称连接端口 (<strong>J2</strong>， <strong>J3</strong>， <strong>J4</strong>， <strong>J6</strong>)。</p>
<p>0 断开连接的所有端口。</p></td>
</tr>
<tr class="odd">
<td>设备命令</td>
<td><strong>/getPort</strong></td>
<td>读取当前连接的端口。</td>
</tr>
<tr class="even">
<td>设备命令
<p>读取电流/电压信息</p></td>
<td><p><strong>/volts</strong></p>
<p><strong>/amps</strong></p>
<p><strong>/version</strong></p></td>
<td><p>读取当前电压。</p>
<p>读取当前电流。</p>
<p>读取设备版本。</p></td>
</tr>
<tr class="odd">
<td>设备命令
<p>启用 SuperSpeed</p></td>
<td><strong>/SuperSpeedOn</strong></td>
<td>为当前和未来连接之前全局允许 SuperSpeed <strong>/SuperSpeedOff</strong>发送命令。
<p>默认情况下启用 superSpeed。</p>
<p>如果 SuperSpeed 处于禁用状态，并且已连接端口 1 或 2，此命令会触发 SuperSpeed 登录时重新连接。</p></td>
</tr>
<tr class="even">
<td>设备命令
<p>禁用 SuperSpeed</p></td>
<td><strong>/SuperSpeedOff</strong></td>
<td>为当前和未来连接之前全局禁用 SuperSpeed <strong>/SuperSpeedOn</strong>发送命令或重置设备。
<p>如果启用了 SuperSpeed 且端口 1 或 2 已连接，此命令禁用 SuperSpeed 行触发重新连接。</p></td>
</tr>
<tr class="odd">
<td><p>集的命令延迟</p></td>
<td><strong>/setDelay</strong> <em>t</em></td>
<td>设置命令延迟<em>t</em>以秒为单位。
<p>设置命令延迟将导致下一步<strong>/setPort</strong>或<strong>/SuperSpeed {打开/关闭}</strong>命令以通过延迟<em>t</em>秒 where <strong>t</strong>范围是从 0 到 99 之间。 这是一次性的设置，仅在下一个命令延迟。 不支持延迟计时器过期前发送多个命令。</p></td>
</tr>
<tr class="even">
<td><p>设置断开连接超时以毫秒为单位</p></td>
<td><strong>/setDisconnectTimeout</strong> <em>t</em></td>
<td>将断开连接超时设置为下一个非零<strong>/setPort</strong>命令。 在下一个连接事件，该端口将仅保持连接状态为<em>t</em>之前断开连接的毫秒。 这是一次性设置，仅下一个连接事件会自动断开连接。 允许的范围是从 0 到 9999 ms。</td>
</tr>
<tr class="odd">
<td><p>批处理命令：</p>
<p>输出到.csv 文件 power 度量值。</p></td>
<td><strong>/powercsv</strong></td>
<td>追加的当前电源度量单位，并为 power.csv 首次运行的时间戳创建 power.csv。 在后续运行将数据追加到此文件。
<p>重命名或删除文件以启动新的数据捕获。 每次运行将追加行采用以下格式： <em>&lt;索引&gt;，&lt;时间&gt;，&lt;伏&gt;，&lt;安培&gt;</em>。</p>
<p><em>索引</em>由给定设备索引<strong>/list</strong>，因此可以同时监视多个设备。</p>
<p><em>时间</em>原始时间戳以秒为单位。</p>
<p><em>伏</em>并<em>安培</em>记录到两个小数位。</p>
<p>此数据可能很长的时间段捕获和绘制在电子表格应用程序，请参阅 cxpower.cmd 脚本。</p></td>
</tr>
<tr class="even">
<td><p>批处理命令：</p>
运行单元测试的主要功能</td>
<td><strong>/test</strong></td>
<td>测试设备的所有主要功能。 用于基本验证设备的功能。 如果此命令会失败，请电源周期的设备，并更新固件。</td>
</tr>
<tr class="odd">
<td><p>批处理命令：</p>
切换序列端口的基本功能演示。</td>
<td><strong>/demo d</strong></td>
<td>循环访问所有端口一次，与<em>d</em>秒的每个端口上的延迟
<p>将端口号、 伏和每个端口上的安培写入到 demoresult.txt。</p></td>
</tr>
</tbody>
</table>



### <a name="sample-commands"></a>示例命令

连接到端口

``` syntax
connexutil.exe /setport 1
```

或者使用的端口名称，如打印在板上：

``` syntax
connexutil.exe /setport J3
```

断开连接的所有端口

``` syntax
connexutil.exe /setport 0
```

循环访问所有端口

``` syntax
for %p in (1 2 3 4) 
do (
    connexutil.exe /setport %p
    echo Confirm device on port %p
    pause
)
```

## <a name="scripts-for-controlling-the-usb-type-c-connex-board"></a>用于控制 USB 类型 C ConnEx 板脚本


这些脚本执行 ConnExUtil.exe 运行顺序，并强调使用 USB 类型 C ConnEx 通过命令行类型测试支持的控件接口。 所有这些脚本支持的可选命令行参数**音频**以指示通过 3.5mm 音频接口已连接 USB 类型 C ConnEx 板。 默认情况下它们只会尝试使用 USB 连接板。

### <a href="" id="cxloop"></a>简单的连接/断开连接序列：CXLOOP.CMD

连接和断开连接 SUT 与每个端口 (1-4)，并提示测试人员将验证该端口上的连接每个端口上暂停。

### <a href="" id="cxstress"></a>随机连接/断开连接循环：CXSTRESS。CMD

连接和断开与每个端口 SUT 随机连接 0.0 5.0 的随机间隔无限循环的秒数。 当它连接的 USB 类型 C 端口随机将启用或禁用 SuperSpeed 连接该端口，并随机将指示要按某些随机间隔 0 到 999 ms 该端口上快速断开连接的看板。

命令行参数**C**将使脚本只能在 USB 类型 C 端口和断开连接的状态之间切换。 数字的命令行参数将重置为以秒为单位输入的值从默认值为 5.0 秒交换机之间的最大随机间隔。 可按任意顺序传递参数。

### <a href="" id="cxpower"></a>长时间运行的功率测量：CXPOWER.CMD

将保存电流和电压 USB 类型 C ConnEx 报告输出文件 power.csv 按 2 的第二个时间间隔。 数据将格式化为逗号分隔的变量，如下所示：

<em>index</em>**,**<em>time</em>**,**<em>volts</em>**,**<em>amps</em>

*索引*由给定设备索引**ConnExUtil.exe /list**命令以便可以同时监视多个设备。

*时间*原始时间戳以秒为单位。

*伏*并*安培*记录到 2 个小数位。

捕获完成后，此数据可能会处理到图表来显示随时间推移的功率消耗的文章，例如电池电量的持续时间的功率消耗周期。 数字的命令行参数重置为默认度量间隔为 2 秒的输入值以秒为单位。

##  <a name="about-test-cases"></a>有关测试用例


USB 类型 C 互操作性测试过程分为两个部分： 功能测试 (FT) 和压力测试 (ST)。 每个测试部分描述了测试用例，并标识适用于测试的类别。 产品必须来测试整个相应的类别。 某些测试用例包含指向相关提示和技巧的其他信息。 本部分侧重于 USB 类型 C 功能和体验。 USB 类型-C 解决方案可能会包含其他 USB 组件，如 USB 集线器或 USB 控制器。 这两个 USB 中介绍了详细的测试信息的 USB 集线器和控制器-如果的[xHCI 互操作性测试过程](https://go.microsoft.com/fwlink/p/?LinkId=623257)和 Windows 硬件认证工具包。

这些测试用例基于 ConnExUtil 命令和示例脚本[脚本，用于控制 USB 类型 C ConnEx 板](#scripts)。 测试用例的脚本，请参阅。 自定义所需的测试方案的脚本。

<a href="" id="device-enumeration"></a>[设备枚举](#ft1)  
确认设备枚举的核心方面都是功能。

<a href="" id="alternate-mode-negotiation"></a>[备用模式协商](#ft2)  
确认受支持的其他模式。

<a href="" id="charging-and-power-delivery--pd-"></a>[计费和电源传递 (PD)](#ft3)  
确认充电与 USB 类型。

<a href="" id="role-swap"></a>[角色切换](#ft4)  
确认角色交换。

压力测试部分说明压力和边缘的情况下，这段时间内测试设备稳定性的过程。 压力测试，则需要自定义设备 (该 SuperMUTT) 旧 USB 验证 (非 USB 类型 C)。 可以使用即将发布的 USB 类型 C 测试设备实现进一步的测试和自动化。

<a href="" id="device-enumeration"></a>[设备枚举](#st1)  
确认设备枚举的核心方面都是功能。

<a href="" id="charging-and-power-delivery--pd-"></a>[计费和电源传递 (PD)](#st2)  
确认充电与 USB 类型。

## <a name="ft-case-1-device-enumeration"></a>FT 案例 1:设备枚举


![ft 案例 1： 设备枚举](images/ft1.png)

| 端口   | 设备                                                                              |
|--------|-------------------------------------------------------------------------------------|
| **J1** | SUT。                                                                                |
| **J2** | 通过使用 USB 类型 C 电缆连接的 USB 类型 C 端口的 PC。              |
| **J3** | USB 类型 C 充电器。                                                                 |
| **J4** | 下游连接用鼠标的 USB 集线器 （SuperSpeed 或高速度）。               |
| **J6** | 通过使用 USB 类型 A 到 B USB 微电缆连接的 USB 端口键入一个线与 PC。 |



1.  关闭 SUT 的电源。
2.  连接到端口标记为 SUT **J1** USB 类型 C ConnEx 上。
3.  将代理控制器连接到 USB 类型 C ConnEx。
4.  连接到 USB 类型 C ConnEx 外围设备。
5.  SUT 并登录到 Windows 上的电源。
6.  在提升的命令提示符处，运行 CXLOOP。CMD 脚本。 脚本暂停时，确认新激活的外围设备可正常运行。
7.  反向 USB 类型 C 电缆的方向，并重复步骤 5-7。

配置与步骤 2-4 相关映像，请参阅[开始...](#config).

## <a name="ft-case-2-alternate-mode-negotiation"></a>FT 案例 2:备用模式协商


![ft 案例 2： 备用模式协商](images/ft2.png)

| 端口   | 设备                                                                              |
|--------|-------------------------------------------------------------------------------------|
| **J1** | SUT。                                                                                |
| **J2** | DisplayPort 到 USB 类型 C 硬件保护装置。                                                   |
| **J3** | USB 类型 C 充电器。                                                                 |
| **J4** | 下游连接使用闪存驱动器的 USB 集线器 （SuperSpeed 或高速度）。         |
| **J6** | 通过使用 USB 类型 A 到 B USB 微电缆连接的 USB 端口键入一个线与 PC。 |



1.  关闭 SUT 的电源。
2.  连接到端口标记为 SUT **J1** USB 类型 C ConnEx 上。
3.  将代理控制器连接到 USB 类型 C ConnEx。
4.  连接到 USB 类型 C ConnEx 外围设备。
5.  SUT 并登录到 Windows 上的电源。
6.  在提升的命令提示符处，运行 CXLOOP。CMD 脚本。 脚本暂停时，确认新激活的外围设备可正常运行。
7.  反向 USB 类型 C 电缆的方向，并重复步骤 5-7。

配置与步骤 2-4 相关映像，请参阅[开始...](#config).

## <a name="ft-case-3-charging-and-power-delivery-pd"></a>FT 案例 3:计费和电源传递 (PD)


![ft 案例 3： 充电和电源传递 (pd)](images/ft3.png)

| 端口   | 设备               |
|--------|----------------------|
| **J1** | SUT。                 |
| **J2** | 无。                |
| **J3** | USB 类型 C 充电器。  |
| **J4** | USB 鼠标。           |
| **J6** | USB Micro B 充电器。 |



1.  关闭 SUT 的电源。
2.  连接到端口标记为 SUT **J1** USB 类型 C ConnEx 上。
3.  将代理控制器连接到 USB 类型 C ConnEx。
4.  连接到 USB 类型 C ConnEx 外围设备。
5.  SUT 并登录到 Windows 上的电源。
6.  在提升的命令提示符处，运行 CXLOOP。CMD 脚本。 脚本暂停时，确认新激活的外围设备可正常运行。
7.  反向 USB 类型 C 电缆的方向，并重复步骤 5-7。
8.  连接到端口 USB 类型 C ConnEx **J2**。

    **ConnExUtil.exe /setPort 2**

9.  如果 SUT 包含多个 USB 类型 C 端口，使用 USB 类型 C 电缆连接同一系统上的两个 USB 类型 C 端口。

    确认，SUT 未在充电 （自身）。

    确认 power LCD 读取与墙上的适配器的预期要求匹配。

10. 替换为连接到 USB 类型 C 充电器**J3**使用不同制造商提供的另一个 USB 类型 C 充电器。

    确认设备接收当前。

配置与步骤 2-4 相关映像，请参阅[开始...](#config).

## <a name="ft-case-4-role-swap"></a>FT 情况 4:角色切换


![ft 用例 4： 角色交换](images/ft4.png)

| 端口   | 设备                                                                              |
|--------|-------------------------------------------------------------------------------------|
| **J1** | SUT。                                                                                |
| **J2** | 通过使用 USB 类型 C 电缆连接的 USB 类型 C 端口的 PC。              |
| **J3** | 无。                                                                               |
| **J4** | USB 闪存驱动器。                                                                    |
| **J6** | 通过使用 USB 类型 A 到 B USB 微电缆连接的 USB 端口键入一个线与 PC。 |



1.  关闭 SUT 的电源。
2.  连接到端口标记为 SUT **J1** USB 类型 C ConnEx 上。
3.  将代理控制器连接到 USB 类型 C ConnEx。
4.  连接到 USB 类型 C ConnEx 外围设备。
5.  SUT 并登录到 Windows 上的电源。
6.  在提升的命令提示符处，运行 CXLOOP。CMD 脚本。 脚本暂停时，确认新激活的外围设备可正常运行。
7.  反向 USB 类型 C 电缆的方向，并重复步骤 5-7。
8.  连接到端口 USB 类型 C ConnEx **J2**。

    确认角色交换。 LCD 屏幕上显示电流指示 power 角色。 **+ ve**如果**J1**是电源的接收器;**-ve**如果**J1**是电源。

9.  执行必要的步骤来交换数据角色并确认每个系统的当前角色已更改。

配置与步骤 2-4 相关映像，请参阅[开始...](#config).

## <a name="st-case-1-device-enumeration"></a>ST 案例 1:设备枚举


![st 案例 1： 设备枚举](images/ft1.png)

| 端口   | 设备                                                                              |
|--------|-------------------------------------------------------------------------------------|
| **J1** | SUT。                                                                                |
| **J2** | 通过使用 USB 类型 C 电缆连接的 USB 类型 C 端口的 PC。              |
| **J3** | USB 类型 C 充电器。                                                                 |
| **J4** | 下游连接用鼠标的 USB 集线器 （SuperSpeed 或高速度）。               |
| **J6** | 通过使用 USB 类型 A 到 B USB 微电缆连接的 USB 端口键入一个线与 PC。 |



1.  关闭 SUT 的电源。
2.  连接到端口标记为 SUT **J1** USB 类型 C ConnEx 上。
3.  将代理控制器连接到 USB 类型 C ConnEx。
4.  连接到 USB 类型 C ConnEx 外围设备。
5.  SUT 并登录到 Windows 上的电源。
6.  在提升的命令提示符处，运行 CXSTRESS。12 个小时内的 CMD。

    通过按 Ctrl-c。 终止脚本

7.  执行步骤中所述[FT 案例 1:设备枚举](#ft1)。

配置与步骤 2-4 相关映像，请参阅[开始...](#config).

## <a name="st-case-2-charging-and-power-delivery-pd"></a>ST 案例 2:计费和电源传递 (PD)


![st 案例 2： 充电和电源传递 (pd)](images/ft3.png)

| 端口   | 设备               |
|--------|----------------------|
| **J1** | SUT。                 |
| **J2** | 无。                |
| **J3** | USB 类型 C 充电器。  |
| **J4** | USB 鼠标。           |
| **J6** | USB Micro B 充电器。 |



1.  关闭 SUT 的电源。
2.  连接到端口标记为 SUT **J1** USB 类型 C ConnEx 上。
3.  将代理控制器连接到 USB 类型 C ConnEx。
4.  连接到 USB 类型 C ConnEx 外围设备。
5.  SUT 并登录到 Windows 上的电源。
6.  在提升的命令提示符处，运行 CXSTRESS。12 个小时内的 CMD。 .

    通过按 Ctrl-c。 终止脚本

7.  执行步骤中所述[FT 案例 3:计费和电源传递 (PD)](#ft3)。

配置与步骤 2-4 相关映像，请参阅[开始...](#config).

## <a name="additional-test-resources"></a>其他测试资源


以下功能测试可适用的 USB 类型-C 来提高传统 USB 方案。

| 测试用例                                | 描述                                                                                                                  | 类别             |
|------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|----------------------|
| [系统启动](type.md#ft2)              | 确认该产品未影响正常的系统启动。                                                               | 系统，停靠，设备 |
| [系统电源转换](type.md#ft3) | 测试是否转换系统的能力，从低功率状态唤醒功能不受影响的产品。 | 系统，停靠，设备 |
| [选择性挂起](type.md#ft4)        | 确认的选择性挂起转换。                                                                                  | 停靠设备         |



以下的压力测试可以改编自 SuperMUTT 测试文档，以展开 USB 方案。

| 测试用例                                | 描述                                                     | 类别             |
|------------------------------------------|-----------------------------------------------------------------|----------------------|
| [系统电源转换](type.md#st1) | 测试产品后执行重复的系统电源事件的可靠性。 | 系统，停靠，设备 |
| [传输事件](type.md#st2)          | 生成多个传输和连接事件。              | 系统，停靠，设备 |
| [Plug and Play （即插即用）](type.md#st3)      | 生成各种即插即用的序列。                                | 系统，停靠，设备 |
| [设备拓扑](type.md#st4)          | 测试一系列设备和该产品的拓扑。       | 系统，停靠，设备 |



## <a name="validating-success-or-failure-of-the-tests"></a>验证成功或失败的测试


### <a name="confirming-charging-and-power"></a>确认充电和电源

在 USB 类型 C ConnEx 载入 LCD 显示 power （伏、 安培和方向）。 确认它符合从电源接通电源并主动启用了 USB 类型 C ConnEx 预期。

![确认充电和电源](images/connexc-connect9.png)

### <a name="confirming-device-addition-on-desktops"></a>确认在台式机上的设备添加

1.  标识你的设备连接到 USB 主控制器。
2.  确保新设备出现在设备管理器中的正确节点之下。
3.  有关 USB 3.0 集线器连接到 USB 3.0 端口，会看到两个 hub 设备： 一个 SuperSpeed 以及高速的另一个枚举。

### <a name="confirm-device-removal-on-desktops"></a>确认设备删除台式机上

1.  标识设备在设备管理器。
2.  执行测试步骤，以从系统删除该设备。
3.  确认设备不再存在于设备管理器。
4.  USB 3.0 集线器，请删除这两种设备 （SuperSpeed 和伴随中心）。 未能删除设备在此情况下可能是设备故障，应进行调查的会审的适当的根本原因，所涉及的所有组件。

### <a name="confirm-device-functionality"></a>确认设备功能

-   如果该设备是 USB 集线器，请确保在中心的下一级的设备功能。 验证其他设备，可以连接到中心上的可用端口。
-   如果设备处于 HID 设备，测试其功能。 请确保 USB 键盘类型、 USB 鼠标将光标，移动和游戏设备将游戏控制器的控制面板中正常运行。
-   USB 音频设备必须播放和/或录音。
-   存储设备必须是可访问，并且应该能够将复制的文件有 200 MB 或更大。
-   如果设备具有多个函数，例如扫描和打印，请确保测试扫描和打印功能。
-   如果设备是 USB 类型 C 设备，确认适用 USB 和其他模式是功能。

## <a name="using-etw-to-log-issues"></a>使用 ETW 来记录问题


转到 https://aka.ms/usbtrace有关说明和下载用于捕获从 USB 驱动程序的 ETW 跟踪的脚本。

## <a name="reporting-test-results"></a>报告测试结果


提供这些详细信息：

-   在未通过的测试之前执行的测试 （按顺序） 的列表。
-   该列表必须指定已失败或传递的测试。
-   系统、 设备、 停靠或用于测试的中心。 包括品牌、 型号和 Web 站点，以便我们可以获取其他信息，如有需要。









