---
description: XHCIWMI 是用于诊断的工具。 此工具仅在 Windows 8 上运行，并在设备连接到 xHCI 端口并加载 Microsoft USB 3.0 驱动程序堆栈时收集信息。
title: USB XHCIWMI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4800dec9fe7ff6a6f8a851155018b723e51902d
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968586"
---
# <a name="usb-xhciwmi"></a>USB XHCIWMI


XHCIWMI 是用于诊断的工具。 此工具仅在 Windows 8 上运行，并在设备连接到 xHCI 端口并加载 Microsoft USB 3.0 驱动程序堆栈时收集信息。

## <a name="xhciwmi"></a>XHCIWMI


在提升的命令提示符窗口中运行以下命令：

**Xhciwmi.exe**

该工具在 "命令" 窗口中显示当前的固件修订版本和有关控制器的信息。 运行以下命令，针对已知问题验证控制器和集线器的固件：

**Xhciwmi.exe –验证**

建议使用 **– verify** 选项检查控制器和连接的中心。

## <a name="related-topics"></a>相关主题
[USB 测试工具](usb-test-tools.md)  
[MUTT 软件包中的工具](mutt-software-package.md)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  



