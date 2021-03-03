---
description: MUTT 连接试验类型 C (USB Type-C ConnEx) 硬件板是 Arduino 板的自定义盾牌。
title: 通过 USB 类型 C ConnEx 测试 USB 类型 C 系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4771061ab8d13dab43385d6cc1a2fa18a5754eee
ms.sourcegitcommit: ac28dd2a921c25796d19572a180b88e460420488
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2021
ms.locfileid: "101682310"
---
# <a name="test-usb-type-c-systems-with-usb-type-c-connex"></a>通过 USB 类型 C ConnEx 测试 USB 类型 C 系统

## <a name="summary"></a>总结

- 使用 USB 类型进行自动测试-C ConnEx
- Windows 10 中的 USB 类型 C 互操作性测试过程：功能测试 (FT) 和压力测试 (ST) 。
- 用于确认方案（如设备添加和删除）的诊断过程和提示。

## <a name="applies-to"></a>适用于

- Windows 10

## <a name="specifications-and-procedures"></a>规范和过程 * *

- [xHCI 互操作性测试过程](https://www.usb.org/document-library/xhci-interoperability-test-procedures-peripherals-hubs-and-hosts-version)

>[!NOTE]
> 某些信息与预发布的产品相关，这些信息可能会在正式发布之前进行重大修改。 Microsoft 不对此处提供的信息作任何明示或默示的担保。

MUTT 连接试验类型 C (USB Type-C ConnEx) 硬件板是 Arduino 板的自定义盾牌。 盾牌提供了一个四对一交换机，用于自动执行 USB 类型 C 方案的互操作性测试。

本主题提供了一些指导原则，用于自动执行以下操作：自动测试系统、设备、与 USB C # 连接器一起停靠，以及与 Windows 操作系统的互操作性。 可以测试属于以下类别之一的硬件：

- 系统：台式机、便携式计算机、平板电脑、服务器或电话，运行具有公开的 USB 类型 C 端口的 Windows 操作系统版本的 SKU。
- Dock：任何 USB 类型为 C 的设备，该设备公开多个端口。
- 设备：任何 USB 设备，都可以连接到系统或插接的类型为 C 的端口。 此类别包括传统 USB 设备以及支持 USB 类型 C 规范中定义的附件和备用模式的设备。

## <a name="hardware-requirements"></a>硬件要求

若要使用 USB 类型-C ConnEx 版本2来执行 USB 类型 C 互操作性测试过程，需要：

- **测试中的系统 (SUT)**

    台式机、便携式计算机、平板电脑、服务器或手机，其中至少有一个公开的类型 C USB 端口。

- **USB 类型-C ConnEx**

    设备有一个男 USB 类型为 C 的端口 (标记为要连接到的 **J1**) 。 该设备还具有四个其他 USB 端口 (标签为 **J2**、 **J3**、 **J4**、 **J6**) 可连接到的设备的设备，这些设备可充当 SUT 的外围设备。 设备监视从 SUT 中提取的 amperage 和电压。 可以从 [MCCI](https://mcci.com/usb/dev-tools/3201-enhanced-type-c-connection-exerciser/)购买必要的硬件。

    ![USB 类型-C ConnEx](images/newconnexc.jpg)

- **外围设备 USB 设备**

    任何 USB 设备，其中包含可附加到 SUT 的 USB 类型 C 端口。 此类别包括传统 USB 设备以及支持 USB 类型 C 规范中定义的备用模式的其他设备。

- **微连接 usb 电缆**

    如果你的 SUT 有 USB A 端口，你将使用此电缆将 USB Type-C ConnEx 连接到电脑 (，这是你将其连接到) 的位置。

- **代理控制器**

    如果 SUT 没有 USB A 端口，则可以通过使用代理运行测试来控制 USB 类型 C ConnEx。 代理控制器应为辅助台式计算机或便携式计算机。

    代理控制器通过使用辅助 USB 端口将 (与移动 SUT) 通信，以便加载固件。

## <a name="hardware-requirements-for-older-versions"></a>旧版本的硬件要求

若要使用 USB 类型-C ConnEx 版本2来执行 USB 类型 C 互操作性测试过程，需要：

- **测试中的系统 (SUT)**

    台式机、便携式计算机、平板电脑、服务器或手机，其中至少有一个公开的类型 C USB 端口。

- **Arduino 万像素 2560 R3**

    [Arduino 兆位 2560 R3](https://store.arduino.cc/usa/mega-2560-r3) 用作测试设置的微控制器。

    ![显示 Arduino 万像素 2560 R3 板。](images/arduino.png)

- **[Arduino 万像素 2560 R3](https://store.arduino.cc/usa/mega-2560-r3) 微控制器的电源适配器**。

- **USB 类型-C ConnEx**

    盾牌有一个男 USB Type-C 端口 (标签为其连接的 **J1**) 。 此防护板还具有四个其他 USB 端口 (标签为 **J2**、 **J3**、 **J4**、 **J6**) 可以连接到的设备，这些设备可充当 SUT 的外围设备。 盾牌监视从 SUT 提取的 amperage 和电压。 可以从 [MCCI](https://store.mcci.com/products/model-3101-type-c-connection-exerciser?variant=17120953798) 或 [JJG 技术](http://www.jjgtechnologies.com/typecconne.htm)购买此板。

    ![USB 类型-C ConnEx](images/connexc-top.png)

- **USB A 到 B 电缆**

    你将使用此电缆将电脑连接到微控制器，以便将微控制器上的固件更新为运行测试。

- **外围设备 USB 设备**

    任何 USB 设备，其中包含可附加到 SUT 的 USB 类型 C 端口。 此类别包括传统 USB 设备以及支持 USB 类型 C 规范中定义的备用模式的其他设备。

- **USB 充电器**

    USB 类型 C，支持 USB 类型 C 当前要求，并选择性地 [提供 Usb 电源](https://www.usb.org/usb-charger-pd#:~:text=USB%20Charger%20%28USB%20Power%20Delivery%29%20USB%20has%20evolved,cell%20phones%2C%20MP3%20players%20and%20other%20hand-held%20devices.)。 还需要 **J6** 的 USB 微 B 充电器。

- **代理控制器**

    可以通过使用代理运行测试来控制 USB 类型 C ConnEx。 代理控制器可以是以下实体之一：

  - 辅助台式计算机或便携式计算机。

    代理控制器与移动 SUT 通信，微控制器用于加载固件。

  - 使用辅助 USB 端口的 SUT。
  - 使用 3.5 mm 音频插孔的 SUT。

    在此设置中，你需要：

    - 使用单个 USB 类型 C 端口在 SUTs 上运行测试的 DTMF 防护板。 在完成固件初始闪存后，可以使用 DTMF 从单端口设备控制盾牌，并提供音频插孔。

        ![dtmf 盾牌](images/dtmf.png)

    - 4针用于将 DTMF 盾牌连接到 SUT 的插头到插头音频电缆。 这允许 SUT 在测试期间控制 USB 类型 C 防护板。

        ![3.5 mm 音频插孔](images/audio-jack.png)

## <a name="software-requirements"></a>软件要求

请确保满足以下要求：

- 你的 SUT 必须具有要用于测试互操作性的 Windows 操作系统的版本。
- 代理控制器必须运行 Windows 10。
- [ ![ 下载 mutt](images/download.png)](https://go.microsoft.com/fwlink/p/?LinkId=786621)软件包并在代理控制器上安装最新的 mutt 软件包。
 包是一套工具，用于使用 USB 类型-C ConnEx 运行测试。 它包含用于更新固件、在外围端口之间切换以及发送请求以模拟测试用例的实用程序。 它还包含测试驱动程序包，用于测试总线、其控制器和连接到总线的设备的功能。

- 对于基于 UCSI 的系统，我们强烈建议使用一些其他设置进行测试，以帮助发现 UCSI 固件错误。 此设置将导致 UCSI 固件出现问题，并且强烈建议仅用于测试目的。 请参阅此博客文章中的 [调试 USCI 固件故障](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/Debugging-UCSI-firmware-failures/ba-p/283226) 。

- 安装测试工具需要提升的命令窗口。

    若要打开提升的命令窗口，用户必须是代理控制器上 **Administrators** 组的成员。 若要打开提升的命令提示符窗口，请创建 Cmd.exe 的桌面快捷方式，选择并按住 (或右键单击 Cmd.exe 快捷方式) ，然后选择 " **以管理员身份运行**"。

### <a name="usb-type-c-connex-tools"></a>USB 类型-C ConnEx 工具

下面是 MUTT 软件包中特定于 USB 类型-C ConnEx 的工具。

| 工具 | 说明 |
| --- | --- |
| [ConnExUtil.exe](#connexutilexe) | 用于执行 USB 类型 C ConnEx 功能的命令行工具。 |
| [CxLoop](#cxloop) | 连接每个端口一次并断开连接。 |
| [CxStress](#cxstress) | 随机压力脚本。 |
| [CxPower](#cxpower) | 捕获一段时间内的 power data (电压和 amperage) 并将输出发送到 CSV 文件。 |

有关所有其他工具的信息，请参阅 [MUTT 软件包中的工具](mutt-software-package.md)。

## <a name="get-started-with-the-newest-version"></a>最新版本入门

按照此过程设置测试环境。

 (全新安装程序的 pic) 

此配置将与此映像类似。 请注意，在连接到电脑时，设备上的微 USB 端口提供对 USB 类型 C ConnEx 的控制。

在这些步骤中，你将连接硬件部分，更新微控制器上的固件并验证安装。

1. 如果可用) ，请将微型 usb 插到 ConnEx 的背面，将 USB A 插入代理控制器 (SUT。

2. 用 USB 类型 C ConnEx 固件更新设备。

    - 打开提升的命令提示符窗口。
    - 导航到 MUTT 软件包的位置，如 C： \\ Program Files (x86) \\ USBTest \\ *&lt; &gt;*。
    - 运行以下命令：

        **ConnExUtil.exe – UpdateFirmware**

3. 在设备背面使用连接的 USB 类型-C 线插入 SUT。

4. 将外围设备连接到标记为 **J2**、 **J3**、 **J4**、 **J6** 的 USB 端口。

5. 确保在代理控制器 (SUT 上的 Device Manager 识别设备（如果可用) ）。

## <a name="get-started-with-older-versions"></a>旧版本入门

按照此过程设置测试环境。

![USB 类型-C ConnEx 配置](images/connexc.png)

配置应类似于此图像。 请注意，在连接到电脑时，微控制器上的 USB 类型 C 端口可提供对 USB 类型 C ConnEx 的控制。

在这些步骤中，你将连接硬件部分，更新微控制器上的固件并验证安装。 连接到手机或平板电脑的音频端口时，DTMF 防护板提供对 USB 类型 C ConnEx 的控制。

1. 将微控制器连接到 USB 类型 C 防护板。

    如果 USB 类型 C ConnEx 未汇编，则继续执行步骤1。 如果 USB 类型 C ConnEx 已汇编，则继续执行步骤2。

    > [!CAUTION]
    > 必须小心执行此步骤，因为 pin 非常弯曲。

     1. 通过确保两个板彼此之间的水平，将 USB 类型 C 防护板的 pin 与微控制器上的 receptors 对齐。

        ![对齐 USB 类型的 pin-C ConnEx](images/connexc-align.png)

     2. 轻轻按两个板。 请注意不要在盾牌上弯曲针脚。

        ![组装 USB 类型-C ConnEx](images/connexc-connect.png)

        组装设备应类似于此图：

        ![已连接的 connex-c 板](images/connexc-connect1.png)

2. 使用连接到代理控制器) 或外部电源适配器上的 USB 类型 B (，从附加的微控制器中打开 USB 类型 C ConnEx。 液晶屏显示类似于此图：

    5秒钟后，LCD 显示屏显示当前和电压。

    ![显示 USB 类型 C ConnEx，但不显示 LCD 显示屏上的任何内容](images/connexc-connect2.png)![显示 LCD 显示屏上带有 "4.27 V" 和 "-0.017 A" 的 USB 类型 C ConnEx。](images/connexc-connect3.png)

    如果你没有看到如上图所示的显示，请确保已正确装配设备。

3. 用 USB 类型-C ConnEx 固件更新微控制器。

    - 打开提升的命令提示符窗口。
    - 导航到 MUTT 软件包的位置，如 C： \\ Program Files (x86) \\ USBTest \\ *&lt; &gt;*。
    - 运行以下命令：

        **MuttUtil.exe – UpdateTabFirmware**

4. 将 SUT 插入到防火墙上 (标签为 **J1**) 的男 USB 类型 C 端口。

    **警告**  连接 SUT 时， **J1** 连接器需要额外的支持。 连接器不足以维持设备或自身的权重。

    ![将测试中的系统附加 (sut) ](images/connexc-connect4.png)

5. 将外围设备连接到标记为 **J2**、 **J3**、 **J4**、 **J6** 的 USB 端口。

    ![将外围设备连接到 USB 类型-C ConnEx](images/connexc-connect7.png)

6. 将代理控制器连接到微控制器。

    - 如果代理控制器是台式计算机或便携式计算机，则通过 USB 建立连接。 如前面的图像中所示，将微控制器上的 USB 类型 B 端口连接到代理控制器上的 USB 端口。
    - 如果代理控制器是移动 SUT，请使用音频端口建立连接。 对于此连接，需要 DTMF 盾牌。
        1. 如下图所示，将 DTMF 屏蔽连接到组装的单元：

            ![dtmf 附件](images/connexc-connect6.png)

        2. 使用4针插头到插孔音频电缆将盾牌的音频端口连接到 SUT 上的音频端口。

            设置应类似于此图像：

            ![将测试中的系统 (sut) 与 dtmf 一起附加](images/connexc-connect5.png)

7. 请确保在代理控制器上 Device Manager 识别 USB 类型 C ConnEx。
    1. 右键单击任务栏中的 "启动" 按钮，然后选择 " **Device Manager**"。
    2. 展开 **(com & LPT)** 节点上的端口，并记下微控制器使用的 com 端口。 在此示例中，它已连接到 COM 4。

        ![设备管理器中的 USB 类型-C ConnEx](images/connexc-connect8.png)

## <a name="connexutilexe"></a>ConnExUtil.exe

以下命令行选项 ConnExUtil.exe 支持用于控制 USB Type-C ConnEx 板。

| 用例 | 选项 | 说明 |
| --- | --- | --- |
| **设备发现**</br>列出连接到 USB 类型的所有设备-C ConnEx | /list | 对于 USB 连接的设备，此选项列出设备实例路径。 对于音频连接设备，它会显示 **音频**。</br></br>若要查看音频设备，请将其与 **/all** 参数一起使用。 带有从1开始的索引的列表，可用于输入 **/#** 参数。 |
| **设备选择**</br>选择连接到 USB 类型 C ConnEx 的所有设备，包括音频。 | **/all**  | 可选。</br></br>如果没有此参数，实用工具将处理 USB 连接的设备。 仅当使用音频连接的设备正在使用时，才使用此参数。 音频发现非常耗时且默认情况下处于禁用状态。 |
| **设备选择**</br>选择连接到 USB 类型-C ConnEx "n" 的特定设备。 | **/#***n* | 可选。</br>输入 *n* 是一个从1开始的索引，该索引连接到 USB 类型 C ConnEx，可以使用 **/list** 参数查看这些设备。 如果没有此参数，则默认行为是在所有 USB ConnEx 板上运行每个命令。 |
| **设备命令** | **/setPort** *p* | 切换到指定的端口 *p*。</br></br>通过指定 number (1-4) 或按名称 (**J2**、 **J3**、 **J4**、 **J6**) 来连接端口。</br></br>0断开所有端口的连接。 |
| **设备命令** | **/getPort** | 读取当前连接的端口。 |
| **设备命令** </br>阅读 amperage/电压信息。 | **/volts**</br></br>**/amps**</br></br>**/version** | 读取当前电压。</br></br>阅读当前 amperage。</br></br>阅读设备版本。 |
| **设备命令**</br>启用 SuperSpeed。 | **/SuperSpeedOn** | 在发送 **/SuperSpeedOff** 命令之前，为当前和未来的连接全局启用 SuperSpeed。</br></br>默认情况下，启用 SuperSpeed。</br></br>如果 SuperSpeed 处于禁用状态，并且端口1或2处于连接状态，则此命令将在 SuperSpeed 触发重新连接。 |
| **设备命令**</br>禁用 SuperSpeed | **/SuperSpeedOff** | 在发送 **/SuperSpeedOn** 命令或重置设备之前，为当前和未来的连接禁用全局 SuperSpeed。</br></br>如果启用了 SuperSpeed 并连接了端口1或2，则此命令会触发重新连接，并禁用 SuperSpeed 线路。 |
| **设置命令延迟** | **/setDelay** | 设置 *命令延迟，以秒为单位* 。</br></br>设置命令延迟将导致下一个 **/setPort** 或 **/SuperSpeed{On/Off}** 命令延迟为 *t* 秒，其中 **t** 的范围介于0到99之间。 这是一次性设置，只延迟下一个命令。 不支持在延迟计时器过期之前发送多个命令。 |
| **设置断开连接超时值（毫秒）** | **/setDisconnectTimeout** *t* | 为下一个非零 **/setPort** 命令设置 "断开连接超时"。 在下一个连接事件上，端口将只在断开连接前保持连接状态的 *t* 毫秒。 这是一次性设置，只会自动断开下一个连接事件。 允许的范围为0到9999毫秒。 |
| **批处理命令：**</br>将功率度量输出到 .csv 文件。 | **/powercsv** | 将当前功率度量和时间戳追加到首次运行创建 power.csv power.csv。 后续运行时，会将数据追加到此文件。</br></br>重命名或删除该文件以启动全新数据捕获。 每次运行都会追加以下格式的行： *&lt; index &gt; 、 &lt; time &gt; 、 &lt; 伏特 &gt; 、 &lt; 安培 &gt;*。</br></br>*index* 是 **/list** 给定的设备索引，因此可以同时监视多个设备。</br></br>*时间* 是原始时间戳，以秒为单位。</br></br>*伏特* 和 *安培* 记录到两个小数位。</br></br>此数据可能会在很长一段时间内捕获并在电子表格应用程序中绘制，请参阅 cxpower 脚本。 |
| **批处理命令：**</br>运行主要功能的单元测试 | **/test** | 测试设备的所有主要功能。 用于对设备功能的基本验证。 如果此命令失败，请重启设备并更新固件。 |
| **批处理命令：**</br>端口切换序列的基本演示。 | **/demo** *d* | 循环遍历所有端口一次，每个端口上有 *d* 秒钟的延迟。</br></br>将每个端口的端口号、伏特和安培写入 demoresult.txt。 |

### <a name="sample-commands"></a>示例命令

连接到端口

```console
connexutil.exe /setport 1
```

或者使用板上打印的端口名称：

```console
connexutil.exe /setport J3
```

断开所有端口的连接

```console
connexutil.exe /setport 0
```

遍历所有端口

```console
for %p in (1 2 3 4)
do (
    connexutil.exe /setport %p
    echo Confirm device on port %p
    pause
)
```

## <a name="scripts-for-controlling-the-usb-type-c-connex-board"></a>用于控制 USB Type-C ConnEx 板的脚本

这些脚本行使 ConnExUtil.exe 支持的控制接口，以通过命令行使用 USB 类型 C ConnEx 运行顺序测试和压力类型测试。 所有这些脚本都支持可选的命令行参数 **音频** ，以指示 USB 类型 C ConnEx 板通过 3.5 mm 音频接口连接。 默认情况下，他们只会尝试使用 USB 连接板。

### <a name="simple-connect--disconnect-sequence-cxloopcmd"></a>简单连接/断开序列： CXLOOP。PORT

将 SUT 连接并断开与每个端口 (1-4) 的连接，并在每个端口上暂停，并提示测试人员验证该端口上的连接。

### <a name="random-connect--disconnect-loop-cxstresscmd"></a>随机连接/断开连接循环： CXSTRESS。PORT

在无限循环中，随机连接并从每个端口断开与每个端口的随机连接，以 0.0-5.0 秒为单位。 当连接到 USB 类型 C 端口时，它会在该端口上随机启用或禁用 SuperSpeed 连接，并将在某个随机时间间隔0– 999 ms 内随机指示该面板在该端口上快速断开连接。

命令行参数 **C** 使脚本仅在 USB 类型 C 端口和断开连接状态之间切换。 数值命令行参数将开关的最大随机间隔从默认值5.0 秒重置为输入值（秒）。 可以按任意顺序传递参数。

### <a name="long-running-power-measurement-cxpowercmd"></a>长时间运行的电源测量： CXPOWER。PORT

将 USB Type-C ConnEx 报告的 amperage 和电压保存到输出文件 power.csv 2 秒的间隔。 数据的格式为逗号分隔的变量，如下所示：

**索引**，**时间**，**伏特**，**安培**

*index* 是 **ConnExUtil.exe/list** 命令给定的设备索引，因此可以同时监视多个设备。

*时间* 是原始时间戳，以秒为单位。

*伏特* 和 *安培* 记录到2个小数位。

捕获完成后，这些数据可能会被发布到显示一段时间内电源消耗的图表中，例如，电池电量周期的持续时间。 数值命令行参数将默认的度量间隔2秒重置为输入值（秒）。

## <a name="about-test-cases"></a>关于测试用例

USB 类型 C 互操作性测试过程分为两部分：功能测试 (FT) 和压力测试 (ST) 。 每个测试部分介绍了测试用例并标识了应用于测试的类别。 必须针对整个适用的类别对产品进行测试。 某些测试用例包含指向相关提示的链接和有关其他信息的提示。 本部分重点介绍 USB 类型 C 功能和体验。 USB 类型 C 解决方案可能包含其他 USB 组件，如 USB 集线器或 USB 控制器。 USB [xHCI 互操作性测试过程](https://www.usb.org/document-library/xhci-interoperability-test-procedures-peripherals-hubs-and-hosts-version) 和 Windows 硬件认证工具包中介绍了 usb 集线器和控制器的详细测试。

这些测试用例基于 ConnExUtil 命令和 [用于控制 USB Type-C ConnEx 板](#scripts-for-controlling-the-usb-type-c-connex-board)的示例脚本脚本。 测试用例引用脚本。 根据测试方案的需要自定义脚本。

[设备枚举](#ft-case-1-device-enumeration)  
确定设备枚举的核心方面是否正常工作。

[备用模式协商](#ft-case-2-alternate-mode-negotiation)  
确认支持的备用模式。

[ (PD) 充电和电源交付 ](#ft-case-3-charging-and-power-delivery-pd)  
确认用 USB 类型 C 进行收费。

[角色交换](#ft-case-4-role-swap)  
确认角色交换。

压力测试部分介绍了用于在一段时间内测试设备稳定性的压力和边缘案例方案的过程。 压力测试需要使用自定义设备 (SuperMUTT) ，以实现传统 USB 验证 (非 USB 类型 C) 。 可以通过即将出现的 USB 类型 C 测试设备实现其他测试和自动化。

[设备枚举](#st-case-1-device-enumeration)  
确定设备枚举的核心方面是否正常工作。

[ (PD) 充电和电源交付 ](#st-case-2-charging-and-power-delivery-pd)  
确认用 USB 类型 C 进行收费。

## <a name="ft-case-1-device-enumeration"></a>FT 案例1：设备枚举

![ft 案例1：设备枚举](images/ft1.png)

| 端口 | 设备 |
| --- | ---|
| **J1** | SUT. |
| **J2** | 使用 usb 类型 c 端口连接的 PC，使用 USB 类型 C 电缆进行连接。 |
| **J3** | USB 类型-C 充电器。 |
| **J4** | USB 集线器 (SuperSpeed 或高速) ，其中鼠标连接到下游。 |
| **J6** | 使用 USB 类型的 PC-使用 USB 类型进行连接的端口电缆-A 到 USB 微 B 电缆。 |

1. 关闭 SUT 电源。
2. 将 SUT 连接到 USB 类型-C ConnEx 上标记为 **J1** 的端口。
3. 将代理控制器连接到 USB 类型 C ConnEx。
4. 将外围设备连接到 USB 类型-C ConnEx。
5. 打开并登录到 Windows。
6. 在提升的命令提示符下，运行 CXLOOP。CMD 脚本。 当脚本暂停时，确认新激活的外围设备是否正常运行。
7. 反转 USB 类型 C 电缆的方向，并重复步骤 5-7。

有关与步骤 2-4 相关的配置映像，请参阅 [入门 ...](#get-started)。

## <a name="ft-case-2-alternate-mode-negotiation"></a>FT 案例2：备用模式协商

![ft 案例2：备用模式协商](images/ft2.png)

| 端口 | 设备 |
| --- | --- |
| **J1** | SUT. |
| **J2** | DisplayPort 到 USB 类型-C 转换器。 |
| **J3** | USB 类型-C 充电器。 |
| **J4** | USB 集线器 (SuperSpeed 或高速) ，并将闪存驱动器连接到下游。 |
| **J6** | 使用 USB 类型的 PC-使用 USB 类型进行连接的端口电缆-A 到 USB 微 B 电缆。 |

1. 关闭 SUT 电源。
2. 将 SUT 连接到 USB 类型-C ConnEx 上标记为 **J1** 的端口。
3. 将代理控制器连接到 USB 类型 C ConnEx。
4. 将外围设备连接到 USB 类型-C ConnEx。
5. 打开并登录到 Windows。
6. 在提升的命令提示符下，运行 CXLOOP。CMD 脚本。 当脚本暂停时，确认新激活的外围设备是否正常运行。
7. 反转 USB 类型 C 电缆的方向，并重复步骤 5-7。

有关与步骤 2-4 相关的配置映像，请参阅 [入门 ...](#get-started)。

## <a name="ft-case-3-charging-and-power-delivery-pd"></a>FT 案例3：充电和电源传输 (PD) 

![ft 案例3：充电和电源传输 (pd) ](images/ft3.png)

| 端口 | 设备 |
| --- | --- |
| **J1** | SUT. |
| **J2** | 无。 |
| **J3** | USB 类型-C 充电器。 |
| **J4** | USB 鼠标。 |
| **J6** | USB 微 B 充电器。 |

1. 关闭 SUT 电源。
2. 将 SUT 连接到 USB 类型-C ConnEx 上标记为 **J1** 的端口。
3. 将代理控制器连接到 USB 类型 C ConnEx。
4. 将外围设备连接到 USB 类型-C ConnEx。
5. 打开并登录到 Windows。
6. 在提升的命令提示符下，运行 CXLOOP。CMD 脚本。 当脚本暂停时，确认新激活的外围设备是否正常运行。
7. 反转 USB 类型 C 电缆的方向，并重复步骤 5-7。
8. 将 USB 类型-C ConnEx 连接到端口 **J2**。

    **ConnExUtil.exe/setPort 2**

9. 如果 SUT 包含多个 USB 类型 C 端口，请使用 USB 类型 C 电缆连接同一系统上的两个 USB 类型 C 端口。

    确认 SUT (自身) 不会充电。

    确认电源的液晶屏读数是否与墙壁适配器的预期相符。

10. 将连接到 **J3** 的 Usb 类型 c 充电器替换为其他制造商提供的另一个 Usb 类型 c 充电器。

    确认设备正在接收当前设备。

有关与步骤 2-4 相关的配置映像，请参阅 [入门 ...](#get-started)。

## <a name="ft-case-4-role-swap"></a>FT 案例4：角色交换

![ft 案例4：角色交换](images/ft4.png)

| 端口 | 设备 |
| --- | --- |
| **J1** | SUT. |
| **J2** | 使用 usb 类型 c 端口连接的 PC，使用 USB 类型 C 电缆进行连接。 |
| **J3** | 无。 |
| **J4** | USB 闪存驱动器。 |
| **J6** | 使用 USB 类型的 PC-使用 USB 类型进行连接的端口电缆-A 到 USB 微 B 电缆。 |

1. 关闭 SUT 电源。
2. 将 SUT 连接到 USB 类型-C ConnEx 上标记为 **J1** 的端口。
3. 将代理控制器连接到 USB 类型 C ConnEx。
4. 将外围设备连接到 USB 类型-C ConnEx。
5. 打开并登录到 Windows。
6. 在提升的命令提示符下，运行 CXLOOP。CMD 脚本。 当脚本暂停时，确认新激活的外围设备是否正常运行。
7. 反转 USB 类型 C 电缆的方向，并重复步骤 5-7。
8. 将 USB 类型-C ConnEx 连接到端口 **J2**。

    确认角色交换。 液晶屏屏幕上显示的 Amperage 指示电源角色。 如果 **J1** 是 power 接收器，则 **+ ve** ;如果 **J1** 是电源，则为 **-ve** 。

9. 执行必要的步骤来交换数据角色并确认每个系统的当前角色已更改。

有关与步骤 2-4 相关的配置映像，请参阅 [入门 ...](#get-started)。

## <a name="st-case-1-device-enumeration"></a>ST 案例1：设备枚举

![st 案例1：设备枚举](images/ft1.png)

| 端口 | 设备 |
| --- | --- |
| **J1** | SUT. |
| **J2** | 使用 usb 类型 c 端口连接的 PC，使用 USB 类型 C 电缆进行连接。 |
| **J3** | USB 类型-C 充电器。 |
| **J4** | USB 集线器 (SuperSpeed 或高速) ，其中鼠标连接到下游。  |
| **J6** | 使用 USB 类型的 PC-使用 USB 类型进行连接的端口电缆-A 到 USB 微 B 电缆。 |

1. 关闭 SUT 电源。
2. 将 SUT 连接到 USB 类型-C ConnEx 上标记为 **J1** 的端口。
3. 将代理控制器连接到 USB 类型 C ConnEx。
4. 将外围设备连接到 USB 类型-C ConnEx。
5. 打开并登录到 Windows。
6. 在提升的命令提示符下，运行 CXSTRESS。CMD 长达12小时。

    按 Ctrl-c 终止脚本。

7. 执行 [FT Case 1： Device 枚举](#ft-case-1-device-enumeration)中所述的步骤。

有关与步骤 2-4 相关的配置映像，请参阅 [入门 ...](#get-started)。

## <a name="st-case-2-charging-and-power-delivery-pd"></a>ST 案例2：充电和电源传递 (PD) 

![st 案例2：充电和电源传递 (pd) ](images/ft3.png)

| 端口 | 设备 |
| --- | --- |
| **J1** | SUT. |
| **J2** | 无。 |
| **J3** | USB 类型-C 充电器。  |
| **J4** | USB 鼠标。 |
| **J6** | USB 微 B 充电器。 |

1. 关闭 SUT 电源。
2. 将 SUT 连接到 USB 类型-C ConnEx 上标记为 **J1** 的端口。
3. 将代理控制器连接到 USB 类型 C ConnEx。
4. 将外围设备连接到 USB 类型-C ConnEx。
5. 打开并登录到 Windows。
6. 在提升的命令提示符下，运行 CXSTRESS。CMD 长达12小时。 .

    按 Ctrl-c 终止脚本。

7. 执行 [FT 案例3：充电和电源交付 (PD) ](#ft-case-3-charging-and-power-delivery-pd)中所述的步骤。

有关与步骤 2-4 相关的配置映像，请参阅 [入门 ...](#get-started)。

## <a name="additional-test-resources"></a>其他测试资源

可对 USB 类型 C 进行以下功能测试，以改善传统的 USB 方案。

| 测试用例 | 说明 | 类别 |
| --- | --- | --- |
| [系统启动](type.md#ft2) | 确认产品不会阻止正常的系统引导。 | 系统、停靠、设备 |
| [系统电源转换](type.md#ft3) | 测试系统的电源转换和唤醒功能是否不受低于此产品的影响。 | 系统、停靠、设备 |
| [选择性挂起](type.md#ft4) | 确认选择性挂起转换。 | 停靠、设备 |

可以通过 SuperMUTT 测试文档调整以下压力测试，以扩展 USB 方案。

| 测试用例 | 说明 | 类别 |
| --- | --- | --- |
| [系统电源转换](type.md#st1) | 在重复系统电源事件之后测试产品可靠性。 | 系统、停靠、设备 |
| [传输事件](type.md#st2) | 生成多个传输和连接事件。 | 系统、停靠、设备 |
| [即插即用 (PnP)](type.md#st3) | 生成各种 PnP 序列。 | 系统、停靠、设备 |
| [设备拓扑](type.md#st4) | 使用产品测试一系列设备和拓扑。 | 系统、停靠、设备 |

## <a name="validating-success-or-failure-of-the-tests"></a>验证测试是否成功或失败

### <a name="confirming-charging-and-power"></a>确认充电和电源

USB 类型-C ConnEx 上的板载 LCD 显示电源 (伏特、安培和方向) 。 确认它与接通电源并主动启用 USB 类型 C ConnEx 的电源匹配。

![确认充电和电源](images/connexc-connect9.png)

### <a name="confirming-device-addition-on-desktops"></a>确认台式机上的设备添加

1. 确定设备连接到的 USB 主机控制器。
2. 请确保新设备显示在 Device Manager 中正确的节点下。
3. 对于连接到 USB 3.0 端口的 USB 3.0 集线器，应会看到两个集线器设备：一个在 SuperSpeed 上枚举，另一个以高速连接。

### <a name="confirm-device-removal-on-desktops"></a>确认台式机上的设备删除

1. 在 Device Manager 中标识设备。
2. 执行测试步骤，从系统中删除设备。
3. 确认设备不再存在于 Device Manager 中。
4. 对于 USB 3.0 集线器，请检查是否已删除 (SuperSpeed 和配套中心) 的两个设备。 在这种情况下，删除设备失败可能是设备故障，并应通过与会审适当根本原因所涉及的所有组件进行调查。

### <a name="confirm-device-functionality"></a>确认设备功能

- 如果设备是 USB 集线器，请确保该集线器的下游设备正常运行。 验证其他设备是否可以连接到集线器上的可用端口。
- 如果设备是一个 HID 设备，请测试其功能。 请确保 USB 键盘类型、USB 鼠标在游戏控制器的控制面板上移动光标和游戏设备正常运行。
- USB 音频设备必须播放和/或录制声音。
- 存储设备必须是可访问的，并且应能够复制200MB 或更大的文件。
- 如果设备具有多个功能，例如扫描 & 打印，请确保测试扫描和打印功能。
- 如果设备是 USB 类型 C 设备，请确认适用的 USB 和备用模式是否正常工作。

## <a name="using-etw-to-log-issues"></a>使用 ETW 记录问题

请参阅 [如何使用 Logman 捕获 USB 事件跟踪](./how-to-capture-a-usb-event-trace.md)

## <a name="reporting-test-results"></a>报告测试结果

请提供以下详细信息：

- 测试列表 (按顺序) 在失败测试之前执行。
- 此列表必须指定失败或通过的测试。
- 用于测试的系统、设备、停靠或集线器。 包含品牌、型号和网站，以便我们可以根据需要获取其他信息。