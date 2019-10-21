---
Description: MUTT 连接试验类型 C （USB 类型 C ConnEx）硬件板是 Arduino 板的自定义盾牌。
title: 通过 USB 类型 C ConnEx 测试 USB 类型 C 系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05d948bdfabe342bd941ab77a7c595c64198cadc
ms.sourcegitcommit: 5b0d2b7a3a4efa3bc4f94a769bf41d58d3321d50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72390726"
---
# <a name="test-usb-type-c-systems-with-usb-type-c-connex"></a>通过 USB 类型 C ConnEx 测试 USB 类型 C 系统


**摘要**

-   使用 USB 类型进行自动测试-C ConnEx
-   Windows 10 中的 USB 类型 C 互操作性测试过程：功能测试（FT）和压力测试（ST）。
-   用于确认方案（如设备添加和删除）的诊断过程和提示。

**适用于**

-   Windows 10

**官方规范和过程**

-   [USB 3.1 和 USB 类型-C 规范]( https://go.microsoft.com/fwlink/p/?LinkId=620208)
-   [xHCI 互操作性测试过程](https://go.microsoft.com/fwlink/p/?LinkId=623257)

**上次更新时间**

-   2016 年 2 月

\[Some 的信息与预发布的产品相关，该产品在商业发布之前可能会进行重大修改。 对于此处提供的信息，Microsoft 不做任何明示或默示的担保。\]

MUTT 连接试验类型 C （USB 类型 C ConnEx）硬件板是 Arduino 板的自定义盾牌。 盾牌提供了一个四对一交换机，用于自动执行 USB 类型 C 方案的互操作性测试。

本主题提供了一些指导原则，用于自动执行以下操作：自动测试系统、设备、与 USB C # 连接器一起停靠，以及与 Windows 操作系统的互操作性。 可以测试属于以下类别之一的硬件：

-   系统：台式机、便携式计算机、平板电脑、服务器或电话，运行具有公开的 USB 类型 C 端口的 Windows 操作系统版本的 SKU。
-   Dock：任何 USB 类型为 C 的设备，该设备公开多个端口。
-   设备：任何 USB 设备，都可以连接到系统或插接的类型为 C 的端口。 此类别包括传统 USB 设备以及支持 USB 类型 C 规范中定义的附件和备用模式的设备。

## <a name="hardware-requirements"></a>硬件要求


若要使用 USB 类型 C ConnEx 执行 USB 类型 C 互操作性测试过程，需要：

-   **正在测试的系统（SUT）**

    台式机、便携式计算机、平板电脑、服务器或手机，其中至少有一个公开的类型 C USB 端口。

-   **Arduino 万像素 2560 R3**

    [Arduino 兆位 2560 R3](https://go.microsoft.com/fwlink/p/?LinkId=733526)用作测试设置的微控制器。 可以从[Arduino 商店](https://go.microsoft.com/fwlink/p/?LinkId=733526)购买此板。

    ![arduino](images/arduino.png)

-   **适用于微控制器的电源适配器**。

    有关 Arduino 万像素 2560 R3 板的兼容适配器的信息，[请参阅此站点](https://go.microsoft.com/fwlink/p/?LinkID=733660)。

-   **USB 类型-C ConnEx**

    防护板有一个连接到 SUT 的男 USB 类型 C 端口（标记为**J1**）。 此防护板还具有四个其他 USB 端口（标记为**J2**、 **J3**、 **J4**、 **J6**），可以将这些端口作为设备连接到 SUT。 盾牌监视从 SUT 提取的 amperage 和电压。 可以从[MCCI](https://go.microsoft.com/fwlink/p/?LinkId=733488)或[JJG 技术]( https://go.microsoft.com/fwlink/p/?linkid=618287)购买此板。

    ![USB 类型-C ConnEx](images/connexc-top.png)

-   **USB A 到 B 电缆**

    你将使用此电缆将电脑连接到微控制器，以便将微控制器上的固件更新为运行测试。

-   **外围设备 USB 设备**

    任何 USB 设备，其中包含可附加到 SUT 的 USB 类型 C 端口。 此类别包括传统 USB 设备以及支持 USB 类型 C 规范中定义的备用模式的其他设备。

-   **USB 充电器**

    USB 类型 C，支持 USB 类型 C 当前要求，并选择性地[提供 Usb 电源](https://go.microsoft.com/fwlink/p/?LinkID=623310)。 还需要**J6**的 USB 微 B 充电器。

-   **代理控制器**

    可以通过使用代理运行测试来控制 USB 类型 C ConnEx。 代理控制器可以是以下实体之一：

    -   辅助台式计算机或便携式计算机。

        代理控制器与移动 SUT 通信;用于加载固件的微控制器。

    -   使用辅助 USB 端口的 SUT。
    -   使用 3.5 mm 音频插孔的 SUT。

        在此设置中，你需要：

        -   使用单个 USB 类型 C 端口在 SUTs 上运行测试的 DTMF 防护板。 在完成固件初始闪存后，可以使用 DTMF 从单端口设备控制盾牌，并提供音频插孔。

            ![dtmf 盾牌](images/dtmf.png)

        -   4针用于将 DTMF 盾牌连接到 SUT 的插头到插头音频电缆。 这允许 SUT 在测试期间控制 USB 类型 C 防护板。

            ![3.5 mm 音频插孔](images/audio-jack.png)

## <a name="software-requirements"></a>软件要求


请确保满足以下要求：

-   你的 SUT 必须具有要用于测试互操作性的 Windows 操作系统的版本。
-   代理控制器必须运行 Windows 10。
-   [![download mutt](images/download.png)](https://go.microsoft.com/fwlink/p/?LinkId=786621)软件包并在代理控制器上安装最新的 mutt 软件包。 
 包是一套工具，用于使用 USB 类型-C ConnEx 运行测试。 它包含用于更新固件、在外围端口之间切换以及发送请求以模拟测试用例的实用程序。 它还包含测试驱动程序包，用于测试总线、其控制器和连接到总线的设备的功能。

-   对于基于 UCSI 的系统，我们强烈建议使用一些其他设置进行测试，以帮助发现 UCSI 固件错误。 此设置将导致 UCSI 固件出现问题，并且强烈建议仅用于测试目的。 请参阅此博客文章中的["转换固件无法检查错误"](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/Debugging-UCSI-firmware-failures/ba-p/283226) 。

-   安装测试工具需要提升的命令窗口。

    若要打开提升的命令窗口，用户必须是代理控制器上**Administrators**组的成员。 若要打开提升的命令提示符窗口，请创建 Cmd.exe 的桌面快捷方式，右键单击 Cmd.exe 快捷方式，然后选择 "**以管理员身份运行**"。

### <a name="usb-type-c-connex-tools"></a>USB 类型-C ConnEx 工具

下面是 MUTT 软件包中特定于 USB 类型-C ConnEx 的工具。

| 工具                          | 描述                                                                                          |
|-------------------------------|------------------------------------------------------------------------------------------------------|
| [ConnExUtil](#connexutilexe) | 用于执行 USB 类型 C ConnEx 功能的命令行工具。                                             |
| [CxLoop](#cxloop)         | 连接每个端口一次并断开连接。                                                             |
| [CxStress](#cxstress)     | 随机压力脚本。                                                                            |
| [CxPower](#cxpower)       | 捕获一段时间内的电源数据（电压和 amperage），并将输出发送到 CSV 文件。 |



有关所有其他工具的信息，请参阅[MUTT 软件包中的工具](mutt-software-package.md)。

## <a name="get-started"></a>入门...


按照此过程设置测试环境。

![USB 类型-C ConnEx 配置](images/connexc.png)

配置应类似于此图像。 请注意，在连接到电脑时，微控制器上的 USB 类型 C 端口可提供对 USB 类型 C ConnEx 的控制。

在这些步骤中，你将连接硬件部分，更新微控制器上的固件并验证安装。 连接到手机或平板电脑的音频端口时，DTMF 防护板提供对 USB 类型 C ConnEx 的控制。

1.  将微控制器连接到 USB 类型 C 防护板。

    如果 USB 类型 C ConnEx 未汇编，则继续执行步骤1。 如果 USB 类型 C ConnEx 已汇编，则继续执行步骤2。

    **警告**  ![caution 必须小心执行此步骤 ](images/caution.png)，因为 pin 非常弯曲。



    1.  通过确保两个板彼此之间的水平，将 USB 类型 C 防护板的 pin 与微控制器上的 receptors 对齐。

        ![对齐 USB 类型的 pin-C ConnEx](images/connexc-align.png)

    2.  轻轻按两个板。 请注意不要在盾牌上弯曲针脚。

        ![组装 USB 类型-C ConnEx](images/connexc-connect.png)

        组装设备应类似于此图：

        ![已连接的 connex-c 板](images/connexc-connect1.png)

2.  使用 USB 类型 B （连接到代理控制器）或外部电源适配器，从附加的微控制器中打开 USB 类型 C ConnEx。 液晶屏显示类似于此图：

    5秒钟后，LCD 显示屏显示当前和电压。

    ![固件启动前的 USB 类型-C ConnEx](images/connexc-connect2.png)![固件启动前的 USB 类型-C ConnEx](images/connexc-connect3.png)

    如果你没有看到如上图所示的显示，请确保已正确装配设备。

3.  用 USB 类型-C ConnEx 固件更新微控制器。
    -   打开提升的命令提示符窗口。
    -   导航到 MUTT 软件包的位置，如 C： \\Program Files （x86） \\USBTest \\ *&lt;arch &gt;* 。
    -   运行以下命令：

        **MuttUtil – UpdateTabFirmware**

4.  将 SUT 插入到盾牌上的男 USB 类型 C 端口（标记为**J1**）。

    **警告** 连接 SUT 时， **J1**连接器需要额外的支持。 连接器不足以维持设备或自身的权重。

    ![附加受测系统（sut）](images/connexc-connect4.png)

5.  将外围设备连接到标记为**J2**、 **J3**、 **J4**、 **J6**的 USB 端口。

    ![将外围设备连接到 USB 类型-C ConnEx](images/connexc-connect7.png)

6.  将代理控制器连接到微控制器。
    -   如果代理控制器是台式计算机或便携式计算机，则通过 USB 建立连接。 如前面的图像中所示，将微控制器上的 USB 类型 B 端口连接到代理控制器上的 USB 端口。
    -   如果代理控制器是移动 SUT，请使用音频端口建立连接。 对于此连接，需要 DTMF 盾牌。
        1.  如下图所示，将 DTMF 屏蔽连接到组装的单元：

            ![dtmf 附件](images/connexc-connect6.png)

        2.  使用4针插头到插孔音频电缆将盾牌的音频端口连接到 SUT 上的音频端口。

            设置应类似于此图像：

            ![通过 dtmf 附加测试系统（sut）](images/connexc-connect5.png)

7.  请确保在代理控制器上设备管理器识别 USB 类型 C ConnEx。
    1.  右键单击任务栏中的 "启动" 按钮，然后选择 "**设备管理器**"。
    2.  展开 "**端口" （com & LPT）** 节点，并记下微控制器使用的 COM 端口。 在此示例中，它已连接到 COM 4。

        ![设备管理器中的 USB 类型-C ConnEx](images/connexc-connect8.png)

## <a name="connexutilexe"></a>ConnExUtil


下面是 ConnExUtil 支持的命令行选项，用于控制 USB 类型-C ConnEx 板。

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
<p>列出连接到 USB 类型的所有设备-C ConnEx</p></td>
<td><strong>/list</strong></td>
<td>对于 USB 连接的设备，此选项列出设备实例路径。 对于音频连接设备，它会显示<strong>音频</strong>。
<p>若要查看音频设备，请将其与<strong>/all</strong>参数一起使用。 具有从1开始的索引的列表，可用于输入到<strong>/#</strong>参数。</p></td>
</tr>
<tr class="even">
<td>设备选择
<p>选择连接到 USB 类型 C ConnEx 的所有设备，包括音频。</p></td>
<td><strong>/all</strong></td>
<td>可选。
<p>如果没有此参数，实用工具将处理 USB 连接的设备。 仅当使用音频连接的设备正在使用时，才使用此参数。 音频发现非常耗时且默认情况下处于禁用状态。</p></td>
</tr>
<tr class="odd">
<td>设备选择
<p>选择连接到 USB 类型-C ConnEx "n" 的特定设备。</p></td>
<td><strong>/#</strong> <em>n</em></td>
<td>（可选）
<p>输入<em>n</em>是一个从1开始的索引，该索引连接到 USB 类型 C ConnEx，可以使用<strong>/list</strong>参数查看这些设备。 如果没有此参数，则默认行为是在所有 USB ConnEx 板上运行每个命令。</p></td>
</tr>
<tr class="even">
<td>Device 命令</td>
<td><strong>/setPort</strong> <em>p</em></td>
<td>切换到指定的端口<em>p</em>。
<p>通过指定数字（1-4）或按名称（<strong>J2</strong>、 <strong>J3</strong>、 <strong>J4</strong>、 <strong>J6</strong>）来连接端口。</p>
<p>0断开所有端口的连接。</p></td>
</tr>
<tr class="odd">
<td>Device 命令</td>
<td><strong>/getPort</strong></td>
<td>读取当前连接的端口。</td>
</tr>
<tr class="even">
<td>Device 命令
<p>读取 amperage/电压信息</p></td>
<td><p><strong>/volts</strong></p>
<p><strong>/amps</strong></p>
<p><strong>/version</strong></p></td>
<td><p>读取当前电压。</p>
<p>阅读当前 amperage。</p>
<p>阅读设备版本。</p></td>
</tr>
<tr class="odd">
<td>Device 命令
<p>启用 SuperSpeed</p></td>
<td><strong>/SuperSpeedOn</strong></td>
<td>在发送<strong>/SuperSpeedOff</strong>命令之前，为当前和未来的连接全局启用 SuperSpeed。
<p>默认情况下，启用 SuperSpeed。</p>
<p>如果 SuperSpeed 处于禁用状态，并且端口1或2处于连接状态，则此命令将在 SuperSpeed 触发重新连接。</p></td>
</tr>
<tr class="even">
<td>Device 命令
<p>禁用 SuperSpeed</p></td>
<td><strong>/SuperSpeedOff</strong></td>
<td>在发送<strong>/SuperSpeedOn</strong>命令或重置设备之前，为当前和未来的连接禁用全局 SuperSpeed。
<p>如果启用了 SuperSpeed 并连接了端口1或2，则此命令会触发重新连接，并禁用 SuperSpeed 线路。</p></td>
</tr>
<tr class="odd">
<td><p>设置命令延迟</p></td>
<td><strong>/setDelay</strong> <em>t</em></td>
<td>设置<em>命令延迟，以秒为单位</em>。
<p>设置命令延迟将导致下一个<strong>/setPort</strong>或<strong>/SuperSpeed{On/Off}</strong>命令延迟为<em>t</em>秒，其中<strong>t</strong>的范围介于0到99之间。 这是一次性设置，只延迟下一个命令。 不支持在延迟计时器过期之前发送多个命令。</p></td>
</tr>
<tr class="even">
<td><p>设置断开连接超时值（毫秒）</p></td>
<td><strong>/setDisconnectTimeout</strong> <em>t</em></td>
<td>为下一个非零<strong>/setPort</strong>命令设置 "断开连接超时"。 在下一个连接事件上，端口将只在断开连接前保持连接状态的<em>t</em>毫秒。 这是一次性设置，只会自动断开下一个连接事件。 允许的范围为0到9999毫秒。</td>
</tr>
<tr class="odd">
<td><p>批处理命令：</p>
<p>将功率度量输出到 .csv 文件。</p></td>
<td><strong>/powercsv</strong></td>
<td>将当前功率度量和时间戳追加到 .csv 中第一次运行创建了 power .csv。 后续运行时，会将数据追加到此文件。
<p>重命名或删除该文件以启动全新数据捕获。 每次运行都追加以下格式的行： <em>&lt;index &gt;，&lt;time &gt; &lt;volts</em>&gt; &lt;amps &gt;。</p>
<p><em>index</em>是<strong>/list</strong>给定的设备索引，因此可以同时监视多个设备。</p>
<p><em>时间</em>是原始时间戳，以秒为单位。</p>
<p><em>伏特</em>和<em>安培</em>记录到两个小数位。</p>
<p>此数据可能会在很长一段时间内捕获并在电子表格应用程序中绘制，请参阅 cxpower 脚本。</p></td>
</tr>
<tr class="even">
<td><p>批处理命令：</p>
运行主要功能的单元测试</td>
<td><strong>/test</strong></td>
<td>测试设备的所有主要功能。 用于对设备功能的基本验证。 如果此命令失败，请重启设备并更新固件。</td>
</tr>
<tr class="odd">
<td><p>批处理命令：</p>
端口切换序列的基本演示。</td>
<td><strong>/demo d</strong></td>
<td>循环遍历所有端口一次，每个端口上有<em>d</em>秒的延迟
<p>将每个端口的端口号、伏特和安培写入 demoresult。</p></td>
</tr>
</tbody>
</table>



### <a name="sample-commands"></a>示例命令

连接到端口

``` syntax
connexutil.exe /setport 1
```

或者使用板上打印的端口名称：

``` syntax
connexutil.exe /setport J3
```

断开所有端口的连接

``` syntax
connexutil.exe /setport 0
```

遍历所有端口

``` syntax
for %p in (1 2 3 4) 
do (
    connexutil.exe /setport %p
    echo Confirm device on port %p
    pause
)
```

## <a name="scripts-for-controlling-the-usb-type-c-connex-board"></a>用于控制 USB Type-C ConnEx 板的脚本


这些脚本执行 ConnExUtil 支持的控件接口，以通过命令行使用 USB 类型-C ConnEx 运行顺序测试和压力类型测试。 所有这些脚本都支持可选的命令行参数**音频**，以指示 USB 类型 C ConnEx 板通过 3.5 mm 音频接口连接。 默认情况下，他们只会尝试使用 USB 连接板。

### <a href="" id="cxloop"></a>简单连接/断开序列： CXLOOP。PORT

连接每个端口并将其与每个端口（1-4）断开连接，并在每个端口上暂停，提示测试人员验证该端口上的连接。

### <a href="" id="cxstress"></a>随机连接/断开连接循环： CXSTRESS。PORT

在无限循环中，随机连接并从每个端口断开与每个端口的随机连接，以 0.0-5.0 秒为单位。 当连接到 USB 类型 C 端口时，它会在该端口上随机启用或禁用 SuperSpeed 连接，并将在某个随机时间间隔0– 999 ms 内随机指示该面板在该端口上快速断开连接。

命令行参数**C**使脚本仅在 USB 类型 C 端口和断开连接状态之间切换。 数值命令行参数将开关的最大随机间隔从默认值5.0 秒重置为输入值（秒）。 可以按任意顺序传递参数。

### <a href="" id="cxpower"></a>长时间运行的电源测量： CXPOWER。PORT

保存 USB Type-C ConnEx 报告的 amperage 和电压，以2秒为间隔输出文件。 数据的格式为逗号分隔的变量，如下所示：

<em>索引</em> **，** <em>时间</em> **，** <em>伏特</em> **，** <em>安培</em>

*index*是**ConnExUtil/list**命令给定的设备索引，因此可以同时监视多个设备。

*时间*是原始时间戳，以秒为单位。

*伏特*和*安培*记录到2个小数位。

捕获完成后，这些数据可能会被发布到显示一段时间内电源消耗的图表中，例如，电池电量周期的持续时间。 数值命令行参数将默认的度量间隔2秒重置为输入值（秒）。

##  <a name="about-test-cases"></a>关于测试用例


USB 类型 C 互操作性测试过程分为两部分：功能测试（FT）和压力测试（ST）。 每个测试部分介绍了测试用例并标识了应用于测试的类别。 必须针对整个适用的类别对产品进行测试。 某些测试用例包含指向相关提示的链接和有关其他信息的提示。 本部分重点介绍 USB 类型 C 功能和体验。 USB 类型 C 解决方案可能包含其他 USB 组件，如 USB 集线器或 USB 控制器。 USB [xHCI 互操作性测试过程](https://go.microsoft.com/fwlink/p/?LinkId=623257)和 Windows 硬件认证工具包中介绍了 usb 集线器和控制器的详细测试。

这些测试用例基于 ConnExUtil 命令和[用于控制 USB Type-C ConnEx 板](#scripts-for-controlling-the-usb-type-c-connex-board)的示例脚本脚本。 测试用例引用脚本。 根据测试方案的需要自定义脚本。

<a href="" id="device-enumeration"></a>[设备枚举](#ft-case-1-device-enumeration)  
确定设备枚举的核心方面是否正常工作。

<a href="" id="alternate-mode-negotiation"></a>[备用模式协商](#ft-case-2-alternate-mode-negotiation)  
确认支持的备用模式。

<a href="" id="charging-and-power-delivery--pd-"></a>[充电和电源交付（PD）](#ft-case-3-charging-and-power-delivery-pd)  
确认用 USB 类型 C 进行收费。

<a href="" id="role-swap"></a>[角色交换](#ft-case-4-role-swap)  
确认角色交换。

压力测试部分介绍了用于在一段时间内测试设备稳定性的压力和边缘案例方案的过程。 压力测试需要使用自定义设备（SuperMUTT）进行传统 USB 验证（非 USB 类型 C）。 可以通过即将出现的 USB 类型 C 测试设备实现其他测试和自动化。

<a href="" id="device-enumeration"></a>[设备枚举](#st-case-1-device-enumeration)  
确定设备枚举的核心方面是否正常工作。

<a href="" id="charging-and-power-delivery--pd-"></a>[充电和电源交付（PD）](#st-case-2-charging-and-power-delivery-pd)  
确认用 USB 类型 C 进行收费。

## <a name="ft-case-1-device-enumeration"></a>FT 案例1：设备枚举


![ft 案例1：设备枚举](images/ft1.png)

| 端口   | 设备                                                                              |
|--------|-------------------------------------------------------------------------------------|
| **J1** | SUT.                                                                                |
| **J2** | 使用 usb 类型 c 端口连接的 PC，使用 USB 类型 C 电缆进行连接。              |
| **J3** | USB 类型-C 充电器。                                                                 |
| **J4** | USB 集线器（SuperSpeed 或高速），其中鼠标连接到下游。               |
| **J6** | 使用 USB 类型的 PC-使用 USB 类型进行连接的端口电缆-A 到 USB 微 B 电缆。 |



1.  关闭 SUT 电源。
2.  将 SUT 连接到 USB 类型-C ConnEx 上标记为**J1**的端口。
3.  将代理控制器连接到 USB 类型 C ConnEx。
4.  将外围设备连接到 USB 类型-C ConnEx。
5.  打开并登录到 Windows。
6.  在提升的命令提示符下，运行 CXLOOP。CMD 脚本。 当脚本暂停时，确认新激活的外围设备是否正常运行。
7.  反转 USB 类型 C 电缆的方向，并重复步骤 5-7。

有关与步骤 2-4 相关的配置映像，请参阅[入门 ...](#get-started)。

## <a name="ft-case-2-alternate-mode-negotiation"></a>FT 案例2：备用模式协商


![ft 案例2：备用模式协商](images/ft2.png)

| 端口   | 设备                                                                              |
|--------|-------------------------------------------------------------------------------------|
| **J1** | SUT.                                                                                |
| **J2** | DisplayPort 到 USB 类型-C 转换器。                                                   |
| **J3** | USB 类型-C 充电器。                                                                 |
| **J4** | USB 集线器（SuperSpeed 或高速），闪存驱动器连接到下游。         |
| **J6** | 使用 USB 类型的 PC-使用 USB 类型进行连接的端口电缆-A 到 USB 微 B 电缆。 |



1.  关闭 SUT 电源。
2.  将 SUT 连接到 USB 类型-C ConnEx 上标记为**J1**的端口。
3.  将代理控制器连接到 USB 类型 C ConnEx。
4.  将外围设备连接到 USB 类型-C ConnEx。
5.  打开并登录到 Windows。
6.  在提升的命令提示符下，运行 CXLOOP。CMD 脚本。 当脚本暂停时，确认新激活的外围设备是否正常运行。
7.  反转 USB 类型 C 电缆的方向，并重复步骤 5-7。

有关与步骤 2-4 相关的配置映像，请参阅[入门 ...](#get-started)。

## <a name="ft-case-3-charging-and-power-delivery-pd"></a>FT 案例3：充电和电源交付（PD）


![ft 案例3：充电和电源交付（pd）](images/ft3.png)

| 端口   | 设备               |
|--------|----------------------|
| **J1** | SUT.                 |
| **J2** | 无。                |
| **J3** | USB 类型-C 充电器。  |
| **J4** | USB 鼠标。           |
| **J6** | USB 微 B 充电器。 |



1.  关闭 SUT 电源。
2.  将 SUT 连接到 USB 类型-C ConnEx 上标记为**J1**的端口。
3.  将代理控制器连接到 USB 类型 C ConnEx。
4.  将外围设备连接到 USB 类型-C ConnEx。
5.  打开并登录到 Windows。
6.  在提升的命令提示符下，运行 CXLOOP。CMD 脚本。 当脚本暂停时，确认新激活的外围设备是否正常运行。
7.  反转 USB 类型 C 电缆的方向，并重复步骤 5-7。
8.  将 USB 类型-C ConnEx 连接到端口**J2**。

    **ConnExUtil/setPort 2**

9.  如果 SUT 包含多个 USB 类型 C 端口，请使用 USB 类型 C 电缆连接同一系统上的两个 USB 类型 C 端口。

    确认 SUT 不会充电（本身）。

    确认电源的液晶屏读数是否与墙壁适配器的预期相符。

10. 将连接到**J3**的 Usb 类型 c 充电器替换为其他制造商提供的另一个 Usb 类型 c 充电器。

    确认设备正在接收当前设备。

有关与步骤 2-4 相关的配置映像，请参阅[入门 ...](#get-started)。

## <a name="ft-case-4-role-swap"></a>FT 案例4：角色交换


![ft 案例4：角色交换](images/ft4.png)

| 端口   | 设备                                                                              |
|--------|-------------------------------------------------------------------------------------|
| **J1** | SUT.                                                                                |
| **J2** | 使用 usb 类型 c 端口连接的 PC，使用 USB 类型 C 电缆进行连接。              |
| **J3** | 无。                                                                               |
| **J4** | USB 闪存驱动器。                                                                    |
| **J6** | 使用 USB 类型的 PC-使用 USB 类型进行连接的端口电缆-A 到 USB 微 B 电缆。 |



1.  关闭 SUT 电源。
2.  将 SUT 连接到 USB 类型-C ConnEx 上标记为**J1**的端口。
3.  将代理控制器连接到 USB 类型 C ConnEx。
4.  将外围设备连接到 USB 类型-C ConnEx。
5.  打开并登录到 Windows。
6.  在提升的命令提示符下，运行 CXLOOP。CMD 脚本。 当脚本暂停时，确认新激活的外围设备是否正常运行。
7.  反转 USB 类型 C 电缆的方向，并重复步骤 5-7。
8.  将 USB 类型-C ConnEx 连接到端口**J2**。

    确认角色交换。 液晶屏屏幕上显示的 Amperage 指示电源角色。 如果**J1**是 power 接收器，则 **+ ve** ;如果**J1**是电源，则为 **-ve** 。

9.  执行必要的步骤来交换数据角色并确认每个系统的当前角色已更改。

有关与步骤 2-4 相关的配置映像，请参阅[入门 ...](#get-started)。

## <a name="st-case-1-device-enumeration"></a>ST 案例1：设备枚举


![st 案例1：设备枚举](images/ft1.png)

| 端口   | 设备                                                                              |
|--------|-------------------------------------------------------------------------------------|
| **J1** | SUT.                                                                                |
| **J2** | 使用 usb 类型 c 端口连接的 PC，使用 USB 类型 C 电缆进行连接。              |
| **J3** | USB 类型-C 充电器。                                                                 |
| **J4** | USB 集线器（SuperSpeed 或高速），其中鼠标连接到下游。               |
| **J6** | 使用 USB 类型的 PC-使用 USB 类型进行连接的端口电缆-A 到 USB 微 B 电缆。 |



1.  关闭 SUT 电源。
2.  将 SUT 连接到 USB 类型-C ConnEx 上标记为**J1**的端口。
3.  将代理控制器连接到 USB 类型 C ConnEx。
4.  将外围设备连接到 USB 类型-C ConnEx。
5.  打开并登录到 Windows。
6.  在提升的命令提示符下，运行 CXSTRESS。CMD 长达12小时。

    按 Ctrl-c 终止脚本。

7.  执行[FT Case 1： Device 枚举](#ft-case-1-device-enumeration)中所述的步骤。

有关与步骤 2-4 相关的配置映像，请参阅[入门 ...](#get-started)。

## <a name="st-case-2-charging-and-power-delivery-pd"></a>ST 案例2：充电和电源传递（PD）


![st 案例2：充电和电源传递（pd）](images/ft3.png)

| 端口   | 设备               |
|--------|----------------------|
| **J1** | SUT.                 |
| **J2** | 无。                |
| **J3** | USB 类型-C 充电器。  |
| **J4** | USB 鼠标。           |
| **J6** | USB 微 B 充电器。 |



1.  关闭 SUT 电源。
2.  将 SUT 连接到 USB 类型-C ConnEx 上标记为**J1**的端口。
3.  将代理控制器连接到 USB 类型 C ConnEx。
4.  将外围设备连接到 USB 类型-C ConnEx。
5.  打开并登录到 Windows。
6.  在提升的命令提示符下，运行 CXSTRESS。CMD 长达12小时。 。

    按 Ctrl-c 终止脚本。

7.  执行[FT 案例3：充电和电源交付（PD）](#ft-case-3-charging-and-power-delivery-pd)中所述的步骤。

有关与步骤 2-4 相关的配置映像，请参阅[入门 ...](#get-started)。

## <a name="additional-test-resources"></a>其他测试资源


可对 USB 类型 C 进行以下功能测试，以改善传统的 USB 方案。

| 测试用例                                | 描述                                                                                                                  | 类别             |
|------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|----------------------|
| [系统启动](type.md#ft2)              | 确认产品不会阻止正常的系统引导。                                                               | 系统、停靠、设备 |
| [系统电源转换](type.md#ft3) | 测试系统的电源转换和唤醒功能是否不受低于此产品的影响。 | 系统、停靠、设备 |
| [选择性挂起](type.md#ft4)        | 确认选择性挂起转换。                                                                                  | 停靠、设备         |



可以通过 SuperMUTT 测试文档调整以下压力测试，以扩展 USB 方案。

| 测试用例                                | 描述                                                     | 类别             |
|------------------------------------------|-----------------------------------------------------------------|----------------------|
| [系统电源转换](type.md#st1) | 在重复系统电源事件之后测试产品可靠性。 | 系统、停靠、设备 |
| [传输事件](type.md#st2)          | 生成多个传输和连接事件。              | 系统、停靠、设备 |
| [即插即用（PnP）](type.md#st3)      | 生成各种 PnP 序列。                                | 系统、停靠、设备 |
| [设备拓扑](type.md#st4)          | 使用产品测试一系列设备和拓扑。       | 系统、停靠、设备 |



## <a name="validating-success-or-failure-of-the-tests"></a>验证测试是否成功或失败


### <a name="confirming-charging-and-power"></a>确认充电和电源

USB 类型 C ConnEx 上的板载 LCD 显示电源（伏特、安培和方向）。 确认它与接通电源并主动启用 USB 类型 C ConnEx 的电源匹配。

![确认充电和电源](images/connexc-connect9.png)

### <a name="confirming-device-addition-on-desktops"></a>确认台式机上的设备添加

1.  确定设备连接到的 USB 主机控制器。
2.  请确保新设备显示在设备管理器中正确的节点下。
3.  对于连接到 USB 3.0 端口的 USB 3.0 集线器，应会看到两个集线器设备：一个在 SuperSpeed 上枚举，另一个以高速连接。

### <a name="confirm-device-removal-on-desktops"></a>确认台式机上的设备删除

1.  在设备管理器中标识设备。
2.  执行测试步骤，从系统中删除设备。
3.  确认设备不再存在于设备管理器中。
4.  对于 USB 3.0 集线器，请检查是否已删除这两个设备（SuperSpeed 和配套集线器）。 在这种情况下，删除设备失败可能是设备故障，并应通过与会审适当根本原因所涉及的所有组件进行调查。

### <a name="confirm-device-functionality"></a>确认设备功能

-   如果设备是 USB 集线器，请确保该集线器的下游设备正常运行。 验证其他设备是否可以连接到集线器上的可用端口。
-   如果设备是一个 HID 设备，请测试其功能。 请确保 USB 键盘类型、USB 鼠标在游戏控制器的控制面板上移动光标和游戏设备正常运行。
-   USB 音频设备必须播放和/或录制声音。
-   存储设备必须是可访问的，并且应能够复制200MB 或更大的文件。
-   如果设备具有多个功能，例如扫描 & 打印，请确保测试扫描和打印功能。
-   如果设备是 USB 类型 C 设备，请确认适用的 USB 和备用模式是否正常工作。

## <a name="using-etw-to-log-issues"></a>使用 ETW 记录问题


请参阅 https://aka.ms/usbtrace 获取说明，并下载用于从 USB 驱动程序捕获 ETW 跟踪的脚本。

## <a name="reporting-test-results"></a>报告测试结果


提供以下详细信息：

-   在失败测试之前执行的测试的列表（按顺序）。
-   此列表必须指定失败或通过的测试。
-   用于测试的系统、设备、停靠或集线器。 包含品牌、型号和网站，以便我们可以根据需要获取其他信息。









