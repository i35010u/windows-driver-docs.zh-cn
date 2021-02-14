---
title: Microsoft 蓝牙测试平台-BTVS
description: 蓝牙测试平台 (BTP) 蓝牙虚拟嗅探器。
ms.date: 1/12/2021
ms.localizationpriority: medium
ms.openlocfilehash: 78414264ffdcc30556d685e33044e57af4ef42fb
ms.sourcegitcommit: 76698e25b77af71155e689200c6e0cf817bfd0d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2021
ms.locfileid: "100267477"
---
# <a name="bluetooth-virtual-sniffer-btvsexe"></a>蓝牙虚拟嗅探器 (btvs.exe) 

蓝牙虚拟嗅探器允许用户在前端协议分析系统、Ellisys 蓝牙分析器或 Wireshark 中查看实时 HCI 跟踪。

> [!NOTE]
> 建议使用 Wireshark。

## <a name="bluetooth-virtual-sniffer-command-line-options"></a>蓝牙虚拟嗅探命令行选项

```console
btvs.exe [-Address 127.0.0.1] [-Mode Frontline|Ellisys|Wireshark]  [-Port 24352] [-Remote off|on] [-Service 1|2|3]

    Address     (Ellisys mode only) Specifies the IP address of the machine
                    running Ellisys Bluetooth Analyzer. (Default: 127.0.0.1)

    Mode        Optionally specify whether btvs.exe should generate traces
                    for Frontline, Ellisys, or Wireshark.

    Port        (Ellisys or Wireshark only) Specifies the UDP listen port of the
                    Ellisys Bluetooth Analyzer injection API\Specifies the TCP port
                    for Wireshark. (Default: 24352)

    Remote      (Wireshark only) Specifies whether Wireshark will be on the same machine
                    or run remotely. Off will try to start Wireshark on the same machine. (Default: off)

    Service     (Ellisys mode only) Specifies the HCI Injection Service.
                    1: Primary. 2: Secondary. 3: Tertiary. (Default: 1)
```

所有这些用法都需要打开命令提示符或 Powershell 控制台，并导航到提取的 BTP 文件夹内的 btvs 应用程序。

## <a name="wireshark-operation"></a>Wireshark 操作

假定安装了 Wireshark。

### <a name="usage-for-wireshark-on-same-machine-recommended"></a> (推荐) 在同一台计算机上使用 Wireshark

1. 使用命令 prompt\PowerShell 控制台运行 btvs.exe：  
    `btvs.exe -Mode Wireshark`
2. 如果安装了 Wireshark，则 Wireshark 将自动打开。  
    否则，请手动启动 Wireshark，并提供默认 TCP 管道作为接口：  
    `wireshark -k -i TCP@127.0.0.1:24352`

### <a name="usage-for-wireshark-on-separate-machine"></a>在单独的计算机上使用 Wireshark

1. 使用命令 prompt\Powershell 控制台运行 btvs.exe：  
    `btvs.exe -Mode Wireshark -Remote on`
2. 运行 wireshark 并通过命令行参数传入第一台计算机的 ip 地址，并传入所选端口：  
    `wireshark -k -i TCP@<ip address>:<port>`  
    注意：端口默认值为24352

## <a name="ellisys-bluetooth-analyzer-operation"></a>Ellisys 蓝牙分析器操作

假定安装了 Ellisys。

### <a name="tool-configuration"></a>工具配置

1. 在 `Tools->Options` Ellisys 蓝牙分析器的 "注入 API" 选项卡上，启用 HCI 注入服务。
2. 在 Ellisys 蓝牙分析器中的中配置录制选项 `Record->Recording options` 。 如果只需要 HCI 跟踪，请取消选中下的所有选项 `Wireless Capture` 。

### <a name="ellisys-usage"></a>Ellisys 用法

1. 启动 Ellisys 蓝牙 Analyzer。
2. 选择 " `HCI Overview (injection)` 概览" 选项卡。
3. 单击 `Record`。
4. 在要跟踪的计算机上以 Ellisys 模式运行 btvs.exe：  
    `btvs.exe -Mode Ellisys`  
    a. 或者，如果 Ellisys Bluetooth 分析器在其他计算机上运行，或 Ellisys 中的侦听端口已更改，请在命令行上提供地址或端口 (参阅) 上方的命令行选项。

## <a name="frontline-protocol-analysis-system-operation"></a>前端协议分析系统操作

假定安装了前端。

### <a name="frontline-protocol-analysis-system-usage"></a>前端协议分析系统使用情况

1. `btvs.exe -Mode Frontline`使用命令 prompt\Powershell 控制台在同一台计算机上运行。
2. 单击 `Start Capture` 工具栏上的按钮 (红色按钮) 。
3. 单击 `View->Frame Display` 以显示 HCI 跟踪。
