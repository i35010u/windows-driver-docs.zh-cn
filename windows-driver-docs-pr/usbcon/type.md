---
description: 本主题说明如何测试启用了 USB 类型 C 的系统和 Windows 的互操作性。
title: USB 类型 C 手动互操作性测试过程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e01ae4c98f6e9e81518d6fb389990c806125483
ms.sourcegitcommit: ec7bebe3f94536455e62b372c2a28fe69d1717f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2020
ms.locfileid: "93349703"
---
# <a name="usb-type-c-manual-interoperability-test-procedures"></a>USB 类型 C 手动互操作性测试过程

## <a name="summary"></a>总结

- Windows 10 中的 USB 类型 C 手动互操作性测试过程：功能测试 (FT) 和压力测试 (ST) 。
- 各种测试计划旨在为分配的时间解决特定目的。
- 用于确认方案（如设备添加和删除）的诊断过程和提示。

## <a name="applies-to"></a>适用于

- Windows 10

## <a name="official-specifications-and-procedures"></a>官方规范和过程

- [xHCI 互操作性测试过程](https://www.usb.org/document-library/xhci-interoperability-test-procedures-peripherals-hubs-and-hosts-version)

本主题说明如何测试启用了 USB 类型 C 的系统和 Windows 的互操作性。 它为设备和系统制造商提供准则，使其能够在公开 USB C # C 连接器的系统和设备上执行各种功能和压力测试。 它假定读者熟悉官方的 USB 规范和 xHCI 互操作性测试过程（可从 USB.ORG 下载）。

若要使用 USB 类型 C ConnEx 板运行这些测试，请参阅 [使用 Usb 类型 c ConnEx 测试 Usb 类型 c 系统](test-usb-type-c-systems-with-mutt-connex-c.md)。

测试产品可以属于以下一个或多个类别：

- **系统** ：台式机、便携式计算机、平板电脑、服务器或带有公开的类型 C USB 端口的电话。 系统必须运行 Windows 10 的版本，例如适用于桌面版的 Windows 10 (家庭、专业版、企业版和教育版) 、Windows 10 移动版或其他版本。
- **Dock** ：任何 USB 类型为 C 的设备，该设备公开多个端口。
- **设备** ：任何 USB 设备，都可以连接到系统或插接的类型为 C 的端口。 此类别包括传统 USB 设备以及支持 USB 类型 C 规范中定义的附件和备用模式的设备。

USB 类型 C 互操作性测试过程分为两部分：功能测试 (FT) 和压力测试 (ST) 。 每个测试部分介绍了测试用例并标识了应用于测试的类别。 必须针对整个适用的类别对产品进行测试。 某些测试用例包含指向相关提示的链接和有关其他信息的提示。 本文档重点介绍 USB 类型 C 功能和体验。 USB 类型 C 解决方案可能包含其他 USB 组件，如 USB 集线器或 USB 控制器。 USB [xHCI 互操作性测试过程](https://www.usb.org/document-library/xhci-interoperability-test-procedures-peripherals-hubs-and-hosts-version) 和 Windows 硬件认证工具包中介绍了 usb 集线器和控制器的详细测试。

<a href="" id="device-enumeration"></a>[设备枚举](#ft1)  
确定设备枚举的核心方面是否正常工作。

<a href="" id="system-boot"></a>[系统启动](#ft2)  
确认产品不会阻止正常的系统引导。

<a href="" id="system-power-transitions"></a>[系统电源转换](#ft3)  
测试系统的电源转换和唤醒功能是否不受低于此产品的影响。

<a href="" id="selective-suspend"></a>[选择性挂起](#ft4)  
确认选择性挂起转换。

<a href="" id="dock-identification"></a>[停靠标识](#ft5)  
确认停靠中的设备描述符已正确实现。

<a href="" id="alternate-mode-negotiation"></a>[备用模式协商](#ft6)  
确认支持的备用模式。

<a href="" id="charging-and-power-delivery--pd-"></a>[ (PD) 充电和电源交付 ](#ft7)  
确认用 USB 类型 C 进行收费。

<a href="" id="role-swap"></a>[角色交换](#ft8)  
确认角色交换。

压力测试部分介绍了用于在一段时间内测试设备稳定性的压力和边缘案例方案的过程。 压力测试需要使用自定义设备、 [MICROSOFT USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)，以实现传统 USB 验证 (非 USB 类型 C) 。 可以通过即将出现的 USB 类型 C 测试设备实现其他测试和自动化。

<a href="" id="system-power-transitions"></a>[系统电源转换](#st1)  
在重复系统电源事件之后测试产品可靠性。

<a href="" id="transfer-events"></a>[传输事件](#st2)  
生成多个传输和连接事件

<a href="" id="plug-and-play--pnp-"></a>[即插即用 (PnP) ](#st3)  
生成各种 PnP 序列。

<a href="" id="device-topology"></a>[设备拓扑](#st4)  
使用产品测试一系列设备和拓扑。

## <a name="ft-case-1-device-enumeration"></a><a href="" id="ft1"></a>FT 案例1：设备枚举

适用于： System、dock、device

## <a name="to-confirm-that-device-enumeration-is-functional"></a>确认设备枚举是否正常工作

1. 重新启动测试系统并登录到 Windows。
2. 在测试系统上打开 **设备管理器** 。 从 " **开始** " 中，在 " **搜索** " 文本框中键入 **devmgmt.msc** 。
3. 将设备连接到支持 USB 类型的系统。 必要时，请确保设备已开机或连接到外部电源。
    - 系统：将任何 USB 类型 C 设备连接到系统。
    - 设备：将设备连接到支持 USB 类型的系统。
    - Dock：连接任何支持备用模式的 USB 3.0 设备和任何 USB 类型为 C 的设备，或者连接到插接的 USB 类型 C 附件。 将坞站连接到系统。

4. 确认在 **设备管理器** 中添加了设备节点。 有关详细信息，请参阅 [如何确认设备添加](#add)。
5. 确认插入的设备不出现错误。
6. 如果适用，请断开设备 (和插接) 并观察 **设备管理器** 中的更改。 停靠和设备不应出现在 **设备管理器** 中。 有关详细信息，请参阅 [如何确认设备删除](#remove)。
7. [翻转或反转](#flip) USB 类型 C 电缆的方向，并重复步骤3到步骤6。

## <a name="ft-case-2-system-boot"></a><a href="" id="ft2"></a>FT 案例2：系统启动

适用于：系统、中心、设备

## <a name="to-confirm-that-the-product-under-test-does-not-inhibit-the-normal-system-boot-process"></a>若要确认所测试的产品不会阻止正常的系统启动过程，请执行下面的操作：

1. 重新启动测试系统并登录到 Windows。
2. 将以下 USB 设备连接到具有公开的 USB 类型 C 端口的系统：
    - 系统：通过使用 USB 类型 C 到 USB 类型（如此图中所示），将这些设备连接到公开的系统 USB 类型 C 端口：

        ![usb 类型-c 配置](images/typec4.png)

        - USB 集线器
        - USB 键盘
        - USB 3.0 闪存驱动器
    - Dock：将这些设备连接到正在测试的插接中公开的端口。
        - USB 集线器
        - USB 键盘
        - USB 3.0 闪存驱动器
    - 设备：将设备连接到系统的公开 USB 类型 C 端口。

3. 在测试系统上打开 **设备管理器** 。 从 " **开始** " 中，在 " **搜索** " 文本框中键入 **devmgmt.msc** 。
4. 确认在 **设备管理器** 中添加了设备节点。 有关详细信息，请参阅 [如何确认设备添加](#add)。
5. 重新启动系统;请确保系统关闭并正常启动。 调查系统故障（如果有）。
6. 对于系统或停靠测试，请确认以下各项：
    - UEFI/BIOS 将 u 盘识别为可启动媒体，系统可以从该驱动器启动。
    - 可通过 UEFI/BIOS 识别 USB 键盘，并可用于输入 UEFI/BIOS。

7. 系统启动后，确认设备显示在 **设备管理器** 中，指示它们已正确枚举。
8. 验证所有连接的设备的设备功能。
9. 对于系统，请重复步骤3到步骤8，方法是将 USB 类型 C 插接连接到系统，并将这些设备连接到坞站。
    - USB 集线器
    - USB 键盘
    - USB 3.0 闪存驱动器

## <a name="ft-case-3-system-power-transitions"></a><a href="" id="ft3"></a>FT 案例3：系统电源转换

适用于： System、dock、device

## <a name="to-confirm-that-the-systems-power-transitions-and-wake-up-capability-from-lower-power-states-are-not-affected-by-the-product"></a>确认系统的电源转换与较低电源状态的唤醒功能是否不受产品影响

1. 重新启动测试系统并登录到 Windows。
2. 将 USB 3.0 集线器连接到系统上公开的 USB 类型 C 端口。 有关详细信息，请参阅 [如何将设备连接到系统](#connect)。
3. 将 USB 设备连接到中心。
4. 在测试系统上打开 **设备管理器** 。
5. 确认在 **设备管理器** 中添加了设备。 有关详细信息，请参阅 [如何确认设备添加](#add)。
6. 通过 "开始" 菜单或如下所述的自动化，将系统发送到较低的电源状态，如睡眠或休眠。
7. 从低功耗状态唤醒系统。 如果设备支持远程唤醒，请使用设备唤醒系统。 有关详细信息，请参阅 [系统唤醒故障排除](#wake)。 否则，通过使用 "电源" 按钮或键盘) ，通常 (唤醒系统。
8. 确认设备仍正常工作。 有关详细信息，请参阅 [如何确认设备功能](#function)。

对其他可用系统电源状态重复此测试：睡眠 (S3) 、休眠 (S4) 和混合睡眠。

> [!NOTE]
> 使用 Windows 驱动程序工具包)  (中包含的 pwrtest.exe，以简化到电源状态的过渡。 有关详细信息，请参阅 [PwrTest](../devtest/pwrtest.md)。

## <a name="ft-case-4-selective-suspend"></a><a href="" id="ft4"></a>FT 案例4：选择性挂起

适用范围： Dock、device

### <a name="to-confirm-that-the-device-transitions-to-selective-suspend"></a>确认设备转换为选择性挂起

1. 在测试设备与系统之间连接 USB 总线分析器。 有关详细信息，请参阅， [使用分析器确认选择性挂起](#analyzer)。
2. 启动捕获会话。
3. 允许设备进入选择性挂起。 等待15秒，同时确保设备上没有活动的传输。 例如，如果测试设备是闪存驱动器，请确保未打开任何文件;对于键盘或鼠标，使设备处于空闲状态。
4. 通过执行操作，从选择性挂起状态唤醒设备。 例如，在闪存驱动器上，打开文件;对于键盘，请按某个键或移动鼠标。
5. 在分析器中，验证设备是否进入了选择性挂起状态。

可以从以下来源找到选择性挂起的其他信息：

- [为 HID 启用选择性挂起](/previous-versions/windows/hardware/design/dn613941(v=vs.85)?redirectedfrom=MSDN)
- [基于 USB 的 HID 设备的选择性挂起](../hid/selective-suspend-for-hid-over-usb-devices.md)
- [揭密选择性挂起](https://techcommunity.microsoft.com/t5/microsoft-usb-blog/demystifying-usb-selective-suspend/ba-p/270736)

## <a name="ft-case-5-dock-identification"></a><a href="" id="ft5"></a>FT 事例5：停靠标识

适用于： Dock

1. 重新启动测试系统并登录到 Windows。
2. 将 USB 类型 C 插接连接到系统。
3. 确保已正确确定坞站状态。

> [!NOTE]
> 有关停靠标识的其他信息，请参阅 [2015 WinHEC 幻灯片演示文稿](https://channel9.msdn.com/Events/WinHEC/2015/OWD100) 中的第26节 (大约第26节，主题：将设备标识为插接) 。

## <a name="ft-case-6-alternate-mode-negotiation"></a><a href="" id="ft6"></a>FT 情况6：备用模式协商

适用于： System、dock、device

### <a name="confirm-alternate-mode-negotiation-for-supported-modes"></a>确认支持模式的备用模式协商

1. 重新启动测试系统并登录到 Windows。
2. 在测试系统上打开 **设备管理器** 。 从 " **开始** " 中，在 " **搜索** " 文本框中键入 **devmgmt.msc** 。
3. 将启用备用模式的 USB 类型-C 设备连接到系统上备用模式启用的 USB 类型 C 端口;如有必要，请确保设备和系统共享至少一种备用模式，并且设备已通电或连接到外部电源。

    > [!NOTE]
    > 对于类型-C 连接器/适配器，请确保已打开适当的外围设备并连接到转换器/适配器的非类型 C 端。

4. 确认 "备用模式" 设备已添加到 **设备管理器** 中。 在某些情况下，备用模式设备可能显示为监视设备或其他总线设备。 有关详细信息，请参阅 [如何确认设备添加](#add)。
5. 断开设备并观察 **设备管理器** 中的更改。 集线器和设备不应再出现在 **设备管理器** 中。 有关详细信息，请参阅 [如何确认设备删除](#remove)。
6. [翻转或反转](#flip) USB 类型 C 电缆的方向，并重复步骤2-5。

## <a name="ft-case-7-charging-and-power-delivery-pd"></a><a href="" id="ft7"></a>FT 案例7：充电和电源交付 (PD) 

适用于：系统、停靠、支持 USB 电源传送协议的设备

### <a name="confirm-charging-with-usb-type-c"></a>确认与 USB 类型-C 的充电

1. 按 USB 定义的方式执行 [usb 电源交付测试](https://www.usb.org/document-library/usb-power-delivery-0) 。
2. 重新启动测试系统并登录到 Windows。
3. 对于系统，请执行以下步骤：
    1. 将两个系统与 USB 类型 C 电缆连接。 确认每个系统仅接收最新的。
    2. 如果系统包含多个 USB 类型 C 端口，请使用 USB 类型 C 电缆连接同一系统上的两个 USB 类型 C 端口。 确认系统不会充电 (自身) 。
    3. 如果捆绑) 到系统的 USB 类型 C 端口，则连接捆绑的 USB 类型-C 充电器 (。 确认系统正在充电。
    4. 从其他源中的 USB 类型-C 充电器重复上述步骤3c。
    5. 将 USB 类型-C 设备连接到系统公开的 USB 类型 C 端口。 确认设备正在接收当前设备。

4. 对于扩展，请执行以下步骤：
    1. 将 dock 连接到支持 usb 类型 C 的系统，并附带 USB 类型-C 线。
    2. 确认坞站已连接系统。

5. 对于设备，请执行以下步骤：
    1. 将设备连接到支持 USB 类型 C 的系统。 确认设备从系统接收电源。
    2.  (可选) 将设备设备连接到支持 USB 类型 C 的系统。 确认设备将对系统计费。

## <a name="ft-case-8-role-swap"></a><a href="" id="ft8"></a>FT 事例8：角色交换

适用于： System

### <a name="confirm-role-swap"></a>确认角色交换

1. 重新启动测试系统并登录到 Windows。
2. 将两个系统与 USB 类型 C 电缆连接。
3. 确认每个系统的当前角色。
4. 执行必要的步骤来交换角色。
5. 确认每个系统的当前角色已更改。

## <a name="st-case-1-system-power-transitions"></a><a href="" id="st1"></a>ST 案例1：系统电源转换

适用于： System、dock、device

1. 重新启动测试系统。
2. 插入 USB SuperMUTT 设备以显示 USB 类型 C 端口。
3. [在 (认证) 测试期间，通过 IO 运行 DF-睡眠]( https://go.microsoft.com/fwlink/p/?LinkId=623311)：
4. 使用 USB 类型 C 测试设备重复步骤3。

## <a name="st-case-2-transfer-events"></a><a href="" id="st2"></a>ST 案例2：传输事件

适用于： System、dock、device

1. 重新启动测试系统。
2. 插入 USB SuperMUTT 设备以显示 USB 类型 C 端口。
3. 运行 [DF-重新启动并](/windows-hardware/test/hlk/testref/99c61fa9-e0eb-43ea-a5fc-db5c3cbd9239) 在测试前后进行 IO 重启。
4. 使用 USB 类型 C 测试设备重复步骤3。

## <a name="st-case-3-plug-and-play"></a><a href="" id="st3"></a>ST Case 3：即插即用

适用于： System、dock、device

1. 重新启动测试系统。
2. 插入 USB SuperMUTT 设备以显示 USB 类型 C 端口。
3. 在测试 [前后通过 IO 运行 DF-睡眠和 PnP]( https://go.microsoft.com/fwlink/p/?LinkId=623313) 。
4. 使用 USB 类型 C 测试设备重复步骤3。

## <a name="st-case-4-device-topology"></a><a href="" id="st4"></a>ST Case 4：设备拓扑

适用于： System、dock、device

1. 重新启动测试系统。
2. 通过使用 USB 类型 C A/V 适配器，连接 A/V 适配器的所有端口，以便可以使用下图中所示的所有功能：

    ![显示 U S B 类型 C A/V 适配器配置的关系图。](images/typec5.png)

3. 如果待测试系统中有其他 USB 类型 C 端口，请重复步骤2。
4. 在测试 [期间，通过 IO 运行 DF-睡眠](/windows-hardware/test/hlk/testref/9d87d997-f451-4a3d-852c-90367d4d3864) 。

> [!NOTE]
> 在测试过程中，验证是否没有通过 USB 类型-C A/V 转换器（如视频失真或音频下拉）连接的设备的 glitching。

## <a name="functional-system-interoperability-test-plan"></a><a href="" id="ft-plan"></a>功能系统互操作性测试计划

预期持续时间：20分钟

此计划的目标是确定系统是否可以使用不同类型的外围设备和充电器。 此测试计划侧重于从系统的 OEM 以外的源进行测试。

- 系统： Windows 10Windows 10 system (电脑、平板电脑或手机) ，并显示 USB 类型 C 端口。
- 外设
  - USB 类型-A 到 USB 类型-C 适配器
        - USB 3.0 集线器
        - USB 鼠标
        - USB 3.0 闪存驱动器
  - USB 类型-C 存储驱动器
  - USB 类型 C 视频 (转换器是可接受的) 
- 电源： USB 类型-C 充电器

- 执行 [FT 案例1：](#ft1) USB 类型 C 转换器的设备枚举。 验证每个设备是否按预期枚举和功能。 此图显示了用于测试 USB 类型转换器的建议拓扑。

    ![用于测试 usb 类型转换器的拓扑](images/typec1.png)

- 执行 [FT 案例6：](#ft6) 列表中剩余外设的备用模式协商。 验证每个设备是否按预期枚举和功能。
- 执行 [FT 案例7：充电和电源交付 (PD) ](#ft7) 与 USB 类型 C 充电器。 跳过需要两台计算机的部分，仅验证系统是否能够使用第三方电源适配器 (接受电源) 。

## <a name="usability-system-interoperability-test-plan"></a>可用性系统互操作性测试计划

预期持续时间：60分钟

此计划的目标是确定此系统是否可以执行 USB 类型 C 外设的最常见用户方案。 此测试计划假设已成功完成 [功能系统互操作性测试计划](#ft-plan)中所述的测试。 可用性测试计划侧重于常见用户、系统和设备方案。

- 系统： Windows 10Windows 10 system (电脑、平板电脑或手机) ，并显示 USB 类型 C 端口。
- 外设
  - USB 类型-A 到 USB 类型-C 适配器
        -   USB 3.0 集线器
        -   USB 鼠标
        -   USB 3.0 闪存驱动器
  - USB 类型-C 存储驱动器
  - USB 类型 C 视频 (转换器是可接受的) 
  - USB 类型-C A/V 转换器 (包括视频、USB，甚至可能是单适配器的音频) 
- 电源：来自不同供应商的两个 USB 类型 C 充电器。

- 执行 [FT 案例3：](#ft3) 针对列表中每个外设的系统电源转换，其中包含 USB 到类型-C 转换器。 验证每个设备在系统电源状态更改之前和之后是否按预期方式进行枚举和功能。
  - 将 USB 类型-A 配置为 USB 类型 C 适配器，如以下映像所示：

    ![用于测试 usb 类型转换器的拓扑](images/typec1.png)

  - 配置 USB 类型-C A/V 转换器，如图所示。

    ![usb 类型-c a/v 转换器配置](images/typec2.png)

- 执行 [FT 案例2：](#ft2) 仅使用配置为 USB 类型 C A/V 转换器的系统启动，并验证这些方案：
  - 系统将在所有连接的设备上启动，并通过 USB 类型-C A/V 转换器在连接监视器中显示视频。
  - 系统将从通过 USB 类型-C A/V 转换器附加的 USB 磁盘启动。

## <a name="full-interoperability-test-plan"></a>完全互操作性测试计划

预期持续时间： 180 + 分钟

完整的互操作性测试计划涵盖了较大的一组用户方案。 如果设备的系统正在准备 USB-IF 证书，请运行这些测试。

- 系统
  - Windows 10Windows 10 system (电脑、平板电脑或手机) ，并显示 USB 类型 C 端口。
  - 其他 Windows 10Windows 10 系统 (电脑、平板电脑或手机) ，并显示 USB 类型 C 端口。 系统 (电脑、平板电脑或手机) ，并显示 USB 类型 C 端口。 我们建议从另一个产品线或 OEM 进行系统。
- 外设
  - USB 类型-A 到类型-C adapterUSB 类型-A 到 USB 类型 C 适配器
        -   USB 3.0 集线器
        -   USB 鼠标
        -   USB 3.0 闪存驱动器
  - USB 类型-C 存储驱动器
        - USB 类型 C 视频 (转换器是可接受的) 
        - USB 类型-C A/V 转换器 (将视频、音频和 USB 包含为单个单元) 
- 电源：来自不同供应商的两个 USB 类型 C 充电器。

- 执行所有函数压力测试事例。 此图显示了 USB 类型-C A/V 的建议配置：

    ![usb 类型-c a/v 适配器配置](images/typec3.png)

## <a name="how-to-confirm-device-addition"></a><a href="" id="add"></a>如何确认设备添加

- 确定设备连接到的 USB 主机控制器。
- 请确保新设备显示在 **设备管理器** 中正确的节点下。
- 对于连接到 USB 3.0 端口的 USB 3.0 集线器，应会看到两个设备：一个在 USB 3.0 下游，另一个是全速集线器的下游。

## <a name="how-to-confirm-device-removal"></a><a href="" id="remove"></a>如何确认删除设备

- 在 **设备管理器** 中标识设备。
- 执行测试步骤，从系统中删除设备。
- 确认设备不再存在于 **设备管理器** 中。
- 对于 USB 3.0 集线器，请检查是否已删除 (SuperSpeed 和配套中心) 的两个设备。 在这种情况下，删除设备失败可能是设备故障，并应通过与会审适当根本原因所涉及的所有组件进行调查。

## <a name="how-to-confirm-device-functionality"></a><a href="" id="function"></a>如何确认设备功能

- 如果设备是 USB 集线器，请确保该集线器的下游设备正常运行。 验证其他设备是否可以连接到集线器上的可用端口。
- 如果设备是一个 HID 设备，请测试其功能。 请确保 USB 键盘类型、USB 鼠标在游戏控制器的控制面板上移动光标和游戏设备正常运行。
- USB 音频设备必须播放和/或录制声音。
- 存储设备必须是可访问的，并且应能够复制200MB 或更大的文件。
- 如果设备具有多个功能，例如扫描 & 打印，请确保测试扫描和打印功能。
- 如果设备是 USB 类型 C，请确认适用的 USB 和备用模式是否正常工作。

## <a name="how-to-connect-a-device-to-a-system"></a><a href="" id="connect"></a>如何将设备连接到系统

- 请确保 USB 1.x 设备使用适用于测试设备的 USB 1.x 电缆。
- 如果系统无法识别设备，请尝试使用相同类型的另一条电缆来连接设备，以检查是否有坏电缆或连接器。

## <a name="troubleshooting-system-wake"></a><a href="" id="wake"></a>系统唤醒疑难解答

若要排查无法唤醒系统的设备，请执行以下操作：

- 确认该设备支持唤醒。
- 确认已将设备连接到的主机控制器设置为唤醒系统。

## <a name="troubleshooting-missing-power-states"></a>排除电源状态故障

如果测试系统无法进入睡眠或休眠状态，请确保系统中的所有设备都安装了最新的设备驱动程序。 最常见的原因之一是系统中不支持的视频卡。

## <a name="using-etw-to-log-issues"></a>使用 ETW 记录问题

若要为 USB 2.0 端口启用 ETW，请参阅 [Windows 7 USB core 堆栈中的 etw](https://techcommunity.microsoft.com/t5/microsoft-usb-blog/etw-in-the-windows-7-usb-core-stack/ba-p/270689#:~:text=ETW%20in%20the%20Windows%207%20USB%20core%20stack.,look.%206%20Click%20OK.%207%20Restart%20Netmon.%20)。

若要启用 USB 3.0 日志记录，请改为执行以下命令 (或参阅 [如何使用 Logman 捕获 USB 事件跟踪](how-to-capture-a-usb-event-trace.md)) ：

```console
logman start usbtrace -ets -o usbtrace.etl -nb 128 640 -bs 128
logman update usbtrace -ets -p Microsoft-Windows-USB-UCX Default
logman update usbtrace -ets -p Microsoft-Windows-USB-USBHUB3 Default
```

捕获这些日志后，请执行测试方案。

使用此命令停止跟踪：

```console
logman stop usbtrace -ets
```

## <a name="using-an-analyzer-to-confirm-selective-suspend"></a><a href="" id="analyzer"></a>使用分析器确认选择性挂起

若要分析 USB 2.0 和3.0 流量，需要一个 USB 分析器设备，如 LeCroy Voyager M3i、Advisor T3 或 TotalPhase Beagle 5000。 这些分析器能够捕获和显示确认选择性挂起功能所需的链接状态信息。

例如，使用 TotalPhase 分析器捕获流量后，会在输出中看到类似于以下内容的事件：

![usb 类型-c 分析器](images/typec-analyzer.png)

当某个测试要求设备进入挂起状态时，您应该能够将 &lt; &gt; 上述挂起事件与您预期设备进入挂起状态的时间相关联。

## <a name="using-an-analyzer-to-confirm-lpm-u1-and-u2-transitions"></a>使用分析器确认 LPM U1 和 U2 转换

分析器跟踪应显式显示每个链接状态转换：事件中的语句显示为 "Rx U0- &gt; U2"。 例如，通过使用 LeCroy software，在 " **报表** " 选项卡中选择 " **USB3" 链接状态计时视图** 。 此选项显示时间轴上的链接状态。 请注意，在这种情况下，分析器可能不会正确显示 U1 到 U2 的转换。 你可能会看到链接状态进入 U1，但从 U2 恢复。

## <a name="disabling-selective-suspend-in-device-manager"></a>在设备管理器中禁用选择性挂起

若要在设备管理器中的 USB 设备上禁用选择性挂起，请首先在设备树中查找设备节点。 在此示例中，在如下所示的集线器上禁用选择性挂起：

![显示在 "设备管理器" 中选择的 "通用 U S B 中心" 的屏幕截图。](images/typec-device-mgr.png)

右键单击该设备，然后选择 " **属性** "。 然后选择 " **电源管理** " 选项卡。

![“设备管理器”](images/typec-device-mgr1.png)

若要禁用选择性挂起，请确保清除 " **允许计算机关闭此设备** 以保存电源" 复选框。

## <a name="flipping-or-reversing-the-usb-type-c-cable"></a><a href="" id="flip"></a>翻转或反转 USB 类型-C 线

USB 类型 C 电缆旨在维持用户功能，而不考虑电缆方向。 翻转或反转电缆是通过拔出电缆、旋转180并重新插入电缆来实现的。

## <a name="reporting-test-results"></a>报告测试结果

请提供以下详细信息：

- 测试列表 (按顺序) 在失败测试之前执行。
- 此列表必须指定失败或通过的测试。
- 用于测试的系统、设备、停靠或集线器。 包含品牌、型号和网站，以便我们可以根据需要获取其他信息。