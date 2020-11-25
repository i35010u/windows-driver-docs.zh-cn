---
title: 手动设置通过 USB 3.0 线缆进行的内核模式调试
description: 适用于 Windows 的调试工具支持通过 USB 3.0 电缆进行内核调试。 本主题介绍如何手动设置 USB 3.0 调试。
ms.assetid: 9A9F5DA0-B98A-4C19-A723-67D06B2409B5
ms.date: 05/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: 73b304cfebe1568391c9fdc435c653e4992904ca
ms.sourcegitcommit: 5a73142b3ff11a4f7713de5cfce71b82a5afb5fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "95872251"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-30-cable-manually"></a>手动设置通过 USB 3.0 线缆进行的内核模式调试

适用于 Windows 的调试工具支持通过 USB 3.0 电缆进行内核调试。 本主题介绍如何手动设置 USB 3.0 调试。

运行调试器的计算机称为 *主机计算机*，被调试的计算机称为 *目标计算机*。

通过 USB 3.0 电缆进行调试需要以下硬件：

- USB 3.0 调试电缆。 这是一条 A 交叉电缆，只包含 USB 3.0 线路，无 Vbus。

- 在主计算机上，xHCI (USB 3.0) 主机控制器

- 在目标计算机上，支持调试的 xHCI (USB 3.0) 主机控制器

## <a name="setting-up-the-target-computer"></a>设置目标计算机

1. 在目标计算机上，启动 UsbView 工具。 UsbView 工具包含在 Windows 调试工具中。
2. 在 UsbView 中，找到所有 xHCI 主机控制器。
3. 在 UsbView 中，展开 xHCI 主机控制器的节点。 查找主机控制器上的端口是否支持调试。

    ```console
    [Port1]

    Is Port User Connectable:         yes
    Is Port Debug Capable:            yes
    Companion Port Number:            3
    Companion Hub Symbolic Link Name: USB#ROOT_HUB30#5&32bab638&0&0#{...}
    Protocols Supported:
     USB 1.1:                         no
     USB 2.0:                         no
     USB 3.0:                         yes
    ```

4. 记下要用于调试的 xHCI 控制器的总线、设备和功能号。 UsbView 显示这些数字。 在以下示例中，总线号为48，设备号为0，并且函数号为0。

    ```console
    USB xHCI Compliant Host Controller
    ...
    DriverKey: {36fc9e60-c465-11cf-8056-444553540000}\0020
    ...
    Bus.Device.Function (in decimal): 48.0.0
    ```

5. 确定了支持调试的 xHCI 控制器后，下一步是找到与 xHCI 控制器上的端口关联的物理 USB 连接器。 若要查找物理连接器，请将任何 USB 3.0 设备插入目标计算机上的任何 USB 连接器。 刷新 UsbView 以查看设备所在的位置。 如果 UsbView 显示设备已连接到所选的 xHCI 主机控制器，则已找到可用于 USB 3.0 调试的物理 USB 连接器。

> [!IMPORTANT]
> 使用 bcdedit 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。 完成调试并禁用内核调试之后，可以重新启用安全启动。  

6. 在目标计算机上，以管理员身份打开命令提示符窗口，然后输入以下命令：

   - **bcdedit/debug on**
   - **bcdedit/dbgsettings usb targetname：**<em>targetname</em>

   其中 *TargetName* 是您为目标计算机创建的名称。 请注意， *TargetName* 不必是目标计算机的正式名称;它可以是您创建的任何字符串，只要它满足以下限制：

   - 字符串不得以大写或小写的任意组合包含在 *TargetName* 中任意位置的 "debug"。 例如，如果在 targetname 中的任何位置使用 "调试" 或 "调试"，则调试将不会正常工作。  
   - 字符串中的唯一字符是连字符 (-) 、下划线 (\_) 、数字0到9以及字母 A 到 Z (大写或小写。
   - 字符串的最大长度为24个字符。

7. 在设备管理器找到要用于调试的 USB 控制器。 在 "*常规*" 选项卡上的 "*位置*" 下，显示总线、设备和功能号。 输入此命令：

   **bcdedit/set "{dbgsettings}" busparams** *b.d.f*

   其中， *b*、 *d* 和 *f* 是 USB 主机控制器的总线、设备和功能号。 总线、设备和功能号必须为十进制格式。

   示例：

   **bcdedit/set "{dbgsettings}" busparams 48.0。0**

8. 重新启动目标计算机。

### <a name="disable-power-management"></a>禁用电源管理

在某些情况下，电源转换可能会干扰 USB 3.0 上的调试。 若要避免这些问题，请为 xHCI 主机控制器禁用选择性挂起 (及其用于调试的根中心) 。

1. 在设备管理器中，导航到 xHCI 主机控制器的节点。 右键单击该节点，然后选择 " **属性**"。 如果有 " **电源管理** " 选项卡，请打开该选项卡，并清除 " **允许计算机关闭此设备以节省电源** " 复选框。

2. 在设备管理器中，导航到 xHCI 主机控制器的根集线器的节点。 右键单击该节点，然后选择 " **属性**"。 如果有 " **电源管理** " 选项卡，请打开该选项卡，并清除 " **允许计算机关闭此设备以节省电源** " 复选框。

完成使用 xHCI 主机控制器进行调试后，为 xHCI 主机控制器重新启用选择性挂起。

## <a name="starting-a-debugging-session-for-the-first-time"></a>首次启动调试会话

1. 将通用串行总线 (USB) 3.0 调试电缆连接到在主机和目标计算机上选择进行调试的 USB 3.0 端口。
2. 确定主机计算机上运行的 Windows 的位数 (32 位或64位) 。
3. 在主计算机上，以与主计算机上运行的 Windows 的位数匹配的 "管理员) 的形式打开某一版本的 WinDbg (。 例如，如果主计算机运行的是64位版本的 Windows，请以管理员身份打开该版本的 WinDbg 的64位版本。
4. 在 " **文件** " 菜单上，选择 " **内核调试**"。 在 "内核调试" 对话框中，打开 " **USB** " 选项卡。输入在设置目标计算机时创建的目标名称。 单击“确定”。

此时，将在主计算机上安装 USB 调试驱动程序。 这就是将 WinDbg 的位数与 Windows 的位数相匹配的原因。 安装 USB 调试驱动程序之后，可以使用32位或64位版本的 WinDbg 来执行后续的调试会话。

## <a name="starting-a-debugging-session"></a>启动调试会话

### <a name="using-windbg"></a>使用 WinDbg

在主计算机上，打开 WinDbg。 在 " **文件** " 菜单上，选择 " **内核调试**"。 在 "内核调试" 对话框中，打开 " **USB** " 选项卡。输入在设置目标计算机时创建的目标名称。 单击“确定”。

还可以通过在命令提示符窗口中输入以下命令来启动与 WinDbg 的会话，其中 *TargetName* 是设置目标计算机时创建的目标名称：

**windbg/k usb： targetname =**<em>targetname</em>

### <a name="using-kd"></a>使用 KD

在主计算机上，打开命令提示符窗口并输入以下命令，其中 *TargetName* 是设置目标计算机时创建的目标名称：

**kd/k usb： targetname =**<em>targetname</em>

### <a name="reboot-the-target-computer"></a>重新启动目标计算机

连接调试器后，请重新启动目标计算机。 重新启动计算机的一种方法是在 `shutdown -r -t 0` 管理员的命令提示符下使用命令。

在目标计算机重新启动后，调试器应该会自动连接。

## <a name="troubleshooting"></a>故障排除

### <a name="usb-device-not-recognized"></a>USB 设备无法识别

当插入调试电缆时，如果 windows 通知显示在文本 "USB 设备无法识别" 的主机上，则可能会遇到已知的 USB 3.1 到3.1 兼容性问题。 当调试电缆连接到主机上的 USB 3.1 控制器，以及目标上的 Intel (冰 Lake 或 Tiger Lake) 3.1 USB 控制器时，此问题会影响调试配置。

有关详细信息和处理器型号列表，请参阅 [Ice lake (微处理器) -维基百科](https://en.wikipedia.org/wiki/Ice_Lake_(microprocessor)) 和或 [Tiger Lake (微处理器) -维基百科](https://en.wikipedia.org/wiki/Tiger_Lake_(microprocessor))。 若要查找目标计算机的处理器型号，请打开 "设置" 应用，然后依次指向 "系统" 和 "关于"。 "处理器" 将在 "设备规范" 下列出。

若要验证是否出现此问题，请打开 "设备管理器"，然后在 "通用串行总线控制器" 下查找 "USB 调试连接设备"。 如果找不到此设备，请在 "其他设备" 下检查 "未知设备"。 右键单击设备以打开其 "属性" 页。 "设备状态" 文本框将包含文本 "Windows 已停止此设备，因为它报告了问题。  (代码 43) "和" USB 设备返回了无效的 USB BOS 描述符 "。

若要解决此问题，请在管理员命令提示符下运行以下命令以更改注册表：
```
reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\usbflags\349500E00000 /v SkipBOSDescriptorQuery /t REG_DWORD /d 1 /f
reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\usbflags\045E06560000 /v SkipBOSDescriptorQuery /t REG_DWORD /d 1 /f
```

然后，删除并重新插入调试电缆。

## <a name="related-topics"></a>相关主题

[手动设置内核模式调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)
