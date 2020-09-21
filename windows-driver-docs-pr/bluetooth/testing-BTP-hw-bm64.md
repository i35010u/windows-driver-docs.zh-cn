---
title: Microsoft 蓝牙测试平台-BM.EXE-64-EVB
description: 蓝牙测试平台 (BTP) 支持的硬件 (BM64) 。
ms.assetid: a6beeecb-5967-4e08-bfe2-b8aae26861ad
ms.date: 7/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 65b7678ae6c8908845e0601ecaef3e0883bcd6f2
ms.sourcegitcommit: 6e6189e3b7f2b376607b507220bd538a296f5b4e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2020
ms.locfileid: "90799830"
---
# <a name="bm-64-evb-board"></a>BM.EXE-64-EVB

## <a name="overview"></a>概述

BM.EXE-64-EVB 是一个独立的评估委员会，用于测试 BTP 的音频和配对。 有关 BM64 的优势的详细信息，请参阅 [音频功能无线收发](testing-BTP-hw-audio.md)器。
  
本部分介绍如何设置和使用 BM.EXE-64-EVB 以使用 BTP 进行测试。

![BM.EXE-64-EVB 的照片](images/BM64-EVB-alpha.png)

## <a name="getting-started"></a>入门

若要将 BM.EXE-64-EVB 与 BTP 配合使用，必须从出厂默认值更新 BM64 的固件和 EEPROM 设置。此外，还应更新 PIC 微控制器以确保稳定性。
从 "*文档/软件库/固件*" 选项卡上的[**微芯片**](https://www.microchip.com/wwwproducts/en/BM64)中下载并提取最新的 BM64 软件工具包 (DSPK v 2.1.3 用于此开发) 。

开始之前的一些配置说明：

- 对于使用 external MCU/PC 控制 ** (来运行 BM64 固件、EEPROM 更新、BTP 测试) **
  - SW46 应将所有位置都切换为关闭
  - SW47 应将所有位置都切换为关闭
- 有关使用内部 MCU 控件 ** (运行独立微芯片示例) **
  - 应将 SW46 的所有位置都转换为，以便 #2
  - 应将所有位置切换到 "SW47"
- 仅在将新固件上传到 PIC 微控制器时， **才** 应连接 JP33。
- 应根据当前目标配置 SW9

| 目标 | 1状态 | 2状态 |
| --- | --- | --- |
| 运行应用程序 (BTP 测试)  | OFF | OFF |
| 将新固件上传到 BM64 | ON | ON |
| 将新的 EEPROM 上传到 BM64 | ON | OFF |

> [!NOTE]
>
> - 所有固件和 EEPROM 文件都应该来自 **同一** 软件包。
> - 运行 DSPK 中包含的工具时，运行应用程序的 Microsoft Defender SmartScreen 通知会在首次运行时出现风险。
> 单击 " *详细信息* "，然后 *继续运行*。

## <a name="flashing-firmware-for-the-bm64"></a>BM64 的固件闪烁

本部分将介绍如何为 BM64 上传新固件。 `isupdate.exe`在) 中找到的工具 (`DSPK v2.x.y Package\Tools\FlashUpdate Tool` 用于将新的十六进制文件上传到 BM64。

1. 将 SW9 位置1和2设置为 ON，并确保删除 JP33。
2. 将微 B USB 电缆插入到 EVB) 上标记为 *UART* 的 P3 (。
3. 启动 `isupdate.exe` 工具并选择与 bm.exe-64-EVB 关联的 com 端口 (使用 `Device Manager` ，并查找 * (COM & LPT) *) 的端口。
4. 设置应为 " *115200*"，将 "*映像*数 *" 设置为*" *16*"，将 "*内存*" 设置为 "*闪存*"，*子类型*设置为 "*串行闪存*"。 设置后，单击 " *连接*"。
     - 如果连接正确，则右侧的 " *设备* " 应该用信息和端口连接来填充， *> COM #* 应在底部窗格中。 其外观应类似于下图 (与相应的 COM 端口) 。
     - 给定 *波特率* 仅适用于此示例的默认设备。 如果已发生 EEPROM 更改以修改 BM64 的波特率，请改为使用此新值。

<br>![连接后的 isupdate 照片](images/btp-bm64-isupdate.png)<br>

5. 单击 " *浏览* " 并导航到)  (找到的 DSPK 中的 BM64 十六进制文件 `DSPK v2.x.y Package\Software\Firmware Image\BM64 Firmware` 。 突出显示所有16个文件 (`BT5506_SHS_FLASH.H00` 通过 `BT5506_SHS_FLASH.H15`) 并单击 " *打开*"。
6. 单击 " *更新* " 更新 BM64's 固件。 当更新发生时，底部窗格将显示进度。 **不要中断此进程，这是因为设备损坏的风险。**
7. 完成更新过程后，将在底部窗格中显示*写入内存的结束*时间。 之后，单击 " *断开连接*"。 等待底部窗格中的 " *端口断开连接* " 消息出现。
8. 卸下微 B USB 电缆，将 " **SW9" 位置1和 "2" 设置为 "关**"，然后将微 B usb 插回 P3。

## <a name="updating-eeprom-for-the-bm64"></a>更新 BM64 的 EEPROM

本部分将介绍如何为 BM64 上传新的 EEPROM 参数。 EEPROM 更新过程涉及使用) 中 `UITool_IS206x_012_DualModeSPK_v2.x.y.exe` (的工具 `DSPK v2.x.y Package\Tools\UI Tool` 使用户界面文件可以设置波特率或启用 UART 等参数。 然后，它涉及使用 `DSPTool_IS206X_012_DUALMODESPK2.1_E1.0_V13.exe`) 中 (的工具 `DSPK v2.x.y Package\Tools\DSP Tool` 创建一个 DSP 文件来设置扬声器和输入筛选配置。
生成 UI 和 DSP 文件后，该进程将利用 `MPET.exe` 工具 (在) 中找到 `DSPK v2.x.y Package\Tools\MP_V2.x.y` 要与完整的 EEPROM *ipf* 文件合并的工具。 使用生成的 *ipf* 工具时，将会将 EEPROM 的实际上传到 BM64，并在 `EEPROM_Tool.exe`) 找到 (工具 `DSPK v2.x.y Package\Tools\EEPROM_Tool` 。

按照微芯片提供的 [**指南**](http://ww1.microchip.com/downloads/en/DeviceDoc/50002514B.pdf) 进行操作，以更新 BM64 EEPROM，尤其是第3.4 部分-"配置 BM64 模块" 和 3.5-"更新 EEPROM 参数"。 下面是本指南的一些重要修改：

- 节 3.4.1-"UI 工具配置" 修改：
  - 3.4.1.3：加载开始文本文件 *UITool_IS206x_012_DualModeSPK_v2.x.y_BM64_EVB.txt* UI 参数。
  - 3.4.1.4：如果使用 BM.EXE-64-BM64CLS2 和 "BM64CLS1" （如果使用 BM.EXE-64-EVB-C1 板），请选择 "" 作为 *IC 包* 。
  - 3.4.1.6：更改 *名称片段* 是可选的，并且不会影响使用 (如果发生更改，请确保名称大于0且小于 32 ASCII 字符) 。
  - 3.4.1.12：如果想要使用默认表（如果看板出现严重错误），请勿覆盖现有表。
- 节 3.4.2-"DSP 工具配置" 修改：
  - 3.4.2.1：选择 "IS206X_012_DUALMODESPK2 1_E1 .0" (或类似于 *IC 版本*的) 。
- 节 3.4.3-"MPET 工具配置" 修改：
  - 3.4.3.3：为默认 *bin* 文件选择 IS206X_012_DUALMODESPK2 "1_E1 _1214" (或类似) 。
  - 3.4.3.5：添加和合并在指南的3.4.1 和3.4.2 节中创建的文件。
  - 3.4.3.8：根据所使用的 DPSK 版本，弹出窗口可能不会影响性能。
- 第3.5 部分-"更新 EEPROM 参数" 修改：
  - 3.5.1：在启动前拔下 USB （如果不是已经）。
  - 3.5.5：使用从节3.4.3 生成的*ipf。* 此外，弹出窗口的文件大小可能会出现*警告。* 单击 *"确定"* (这种情况下会同时) 默认表。
  - 3.5.6： **不要中断此进程，这是因为设备损坏的风险**。

## <a name="verifying-installation-with-spkcommand"></a>验证是否已安装 SPKCommand

发生固件和 EEPROM 更新后，可以使用 SPKCOMMAND 中包含的 DSPK 工具来验证与 BTP 通信所需的 BM.EXE-64-EVB 的 UART 消息功能。

1. 将 SW9 位置1和2设置为 OFF，并确保删除 JP33 跳线。
2. 将微 B USB 电缆插入到 EVB) 上标记为 *UART* 的 P3 (。
3. 启动 `SPKCommandSetTool vA.B.exe`) 找到的 (`DSPK v2.x.y Package\Tools\SPKCommandSetTool` 。

  - 将 *端口* 设置为与 bm.exe 64-EVB 关联的 COM 端口。
  - 按照 EEPROM 更新将 *波特率* 设置为 *19200* 。 

4. 单击 " *打开* " 按钮。 消息可能出现在右侧的日志中。
5. 单击 " *信息* " 选项卡，然后单击 " *更新* " 按钮。

  - 如果 UART 消息正确通信，则会在左侧填充 *本地设备名称* 和 *蓝牙地址* 等信息，右侧的日志将显示 *事件：* 和 *命令：* 消息后跟表示 UART 消息内容的十六进制代码。
  - 如果未填充 BM64 信息，并且仅 *命令：* 在日志中显示消息，请尝试关闭并重新打开连接。 如果预期的行为仍未出现，请参阅下面的 [帮助](testing-BTP-hw-bm64.md#further-help) 部分。
<br>

![发送正确的消息后的 SPKCommand 照片](images/btp-bm64-spkcommand.png)

## <a name="using-the-bm-64-evb"></a>使用 BM.EXE-64-EVB

安装新的固件和 EEPROM 后，请确保删除 JP33 跳线，并关闭 SW9 位置1和2。 此外，将 SW46 和 SW47 的所有位置设置为 OFF。 这些设置与 [通过 SPKCommand 验证安装](testing-BTP-hw-bm64.md#verifying-installation-with-spkcommand)中的设置相同。

验证设置后，只需在 EVB) 和测试 *计算机上的* P3 (的 P3 之间连接一个微 B USB 电缆。
或者，3.5 mm 插座耳机或扬声器可以连接到 EVB) 上标记为 *SPK* 的 P7 (，如果在 EEPROM 中启用了音频输出。
如果要使用外部扬声器，则板必须具有15V 圆筒插孔用于为音频 amp 供电。

若要使用 BM.EXE-64-EVB 运行 BTP，请确保在 [设置 BTP software](testing-BTP-setup.md#software-setup)后正确安装软件。 此外，请参阅 [配对测试](testing-BTP-tests-pairing.md) 和 [音频测试](testing-BTP-tests-audio.md) ，以运行 BTP 当前支持的测试，BM.EXE-64-EVB。

## <a name="optional-installing-firmware-for-the-pic-microcontroller"></a> (可选) 为 PIC 微控制器安装固件

本部分将介绍如何为机载 PIC 微控制器上传新固件。 PIC 微控制器仅用于独立微芯片 BM.EXE-64-EVB 示例 (如使用普通按钮控制音乐) ，无需使用 BTP 测试。

> [!NOTE]
>
> - 使用与 BM64 兼容性的固件和 EEPROM 所用的 PIC 微控制器固件相同的 DSPK 版本
> - 通过 [**MPLAB Snap**](https://www.microchip.com/developmenttools/ProductDetails/PartNO/PG164100)实现了这些步骤，但其他 ICSP 兼容的程序员可能会工作。

1. 从微芯片下载 [**MPLAB X IDE/IPE**](https://www.microchip.com/mplab/mplab-x-ide) 。
2. 连接 JP33 上的跳线。 将 SW9 #2 的 "位置 1" 和 "2" 设置为 "关"，应将 "SW46" 的所有位置都转换为 "" 应为 "开"。
3. 将 15V DC 电源适配器插入 P2 插孔，以便为 MCU 提供电源。
4. 将 MPLAB Snap 插到 ICSP Ygs-j5-sar 头中，将 USB 电缆插到 Snap。

  - 请确保方向正确 (在 Ygs-j5-sar 标头) 上，将点对齐到引脚1。
 
5. 打开 `MPLAB X IPE.exe` 并配置给定参数：

  - 对于 " *设备*"，选择 "PIC18F85J10 (目标 MCU) 的产品名称。
  - 对于 " *工具*"，它应在插入到 USB 的情况下由 Snap 自动填充。

6. 如果成功，请单击 " *连接* ("，应在输出屏幕) 找到目标设备。
7. 加载在) 找到的 DSPK (中包含的十六进制文件 `DSPK v2.x.y Package\Software\Firmware Image\PIC18 Image` 。
8. 大多数情况下，在加载 Hex 文件后，会出现一条警告，指出调试位已设置。 如果是这样，请进入菜单并单击 "*设置*" " -> *高级模式*"，然后输入密码。
9. 输入密码 (并且十六进制文件仍然正确加载) 中，单击 " *程序*"。
10. 在成功进行编程后 (校验和应与) 匹配，请单击 " *断开连接* " 并删除对齐。
11. 尝试其他任何函数之前 **，请删除 JP33 跳线**。

## <a name="further-help"></a>更多帮助

如果固件和 EEPROM 更新并 [验证 SPKCommand 的安装](testing-BTP-hw-bm64.md#verifying-installation-with-spkcommand) 不成功，这意味着不会在计算机与 BM64 之间传递 UART 消息。 有几种方法可以尝试更正此问题。

### <a name="confirm-setup-and-power-cycle"></a>确认安装和电源周期

第一个常见问题是，未正确使用用于运行 SPKCommand/BTP 的开关和跳线配置该主板。 要检查的板上的几个关键组件配置如下所示：

- SW9：确保位置1和2均设置为 OFF。
- P3：验证是否已将微 B USB 插入到 *UART* 端口。
- JP33：验证是否已删除跳线。
- SW46：确保所有位置都 (按) 上的 BM64 广播方向切换为关闭状态
- SW47：确保所有位置都 (按) 上的 BM64 广播方向切换为关闭状态

验证这些验证后，拔出并等待至少10秒或更长时间，并 replug。 即使配置正确，unpluging 和插入的电源周期也可能会有所帮助。 之后，再次尝试 [验证 With SPKCommand](testing-BTP-hw-bm64.md#verifying-installation-with-spkcommand) 部分的安装。 如果仍然不起作用，请继续下面的更多建议。

### <a name="using-mspk-spkcommand"></a>使用 MSPK SPKCommand

另一种解决方案是使用不同版本的 SPKCommand。 为此，请在 "*文档/软件库/固件*" 选项卡上从[**微芯片**](https://www.microchip.com/wwwproducts/en/BM64)下载并提取 MSPK v 1.35 BM64 软件工具包。在 MSPK v 1.35 工具包中，找到 `SPKCommandSetTool v192.006.exe`)  (的工具 `BM64 Software & Tools (MSPKv1.35)\Tools\SPK CommandSet Tool` 。 使用 SPKCommand 工具的 MSPK v 1.35 版本通过 [SPKCommand 验证安装](testing-BTP-hw-bm64.md#verifying-installation-with-spkcommand) 中的相同说明。
如果 BM.EXE-64-EVB 使用 MSPK v 1.35 工具正确响应，则可将该板用于 BTP。
