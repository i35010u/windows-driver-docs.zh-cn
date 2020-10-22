---
description: XHCIWMI 是用于诊断的工具。 此工具仅在 Windows 8 上运行，并在设备连接到 xHCI 端口并加载 Microsoft USB 3.0 驱动程序堆栈时收集信息。
title: USB XHCIWMI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 373042d9069af162abdd4cb2c43ef7a81fe28ace
ms.sourcegitcommit: a866b3470025d85b25a48857a81f893179698e7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92356021"
---
# <a name="usb-xhciwmi"></a>USB XHCIWMI

XHCIWMI 是用于诊断的工具。 此工具仅在 Windows 8 上运行，并在设备连接到 xHCI 端口并加载 Microsoft USB 3.0 驱动程序堆栈时收集信息。

## <a name="xhciwmi"></a>XHCIWMI

在提升的命令提示符窗口中运行以下命令：

```console
Xhciwmi.exe
```

该工具在 "命令" 窗口中显示当前的固件修订版本和有关控制器的信息。 运行以下命令，针对已知问题验证控制器和集线器的固件：

```console
Xhciwmi.exe –verify
```

建议使用 **– verify** 选项检查控制器和连接的中心。

## <a name="related-topics"></a>相关主题

[MUTT 软件包中的工具](mutt-software-package.md)  

[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  
