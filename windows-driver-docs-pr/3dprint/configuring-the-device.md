---
title: 配置设备
description: 若要配置设备，你应具有的设备和打印机控制面板中的 3D 打印机设备，并且可以打印到 G 代码使用 Microsoft 切片器。
ms.assetid: 897081C3-47A4-46A0-9A45-A49E4569216D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39f4fc78da8cb0a8d4e282f2bf1b261d35e84d8f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522415"
---
# <a name="configuring-the-device"></a>配置设备


若要配置设备，3D 打印机设备中应有**设备和打印机**控制面板可以打印到 G 代码使用 Microsoft 切片器。

接下来你将需要更改切片器和高级配置文件中的设置。

有两个控制打印机属性和切片器设置的配置文件。

打印到硬件设备时： 

- **C:\\Windows\\System32\\MS3DPrint\\StandardGCode\*。XML** – 这由 StandardGCode.DLL，可以更改设备的具体取决于定义中的注册表映射**配置 Xml**密钥下：

    - 每个打印机队列：HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\3DPRINTER\\{PrinterName}\\{node}

    - 每个硬件 ID:HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\USB\\{VID&PID}\\{DeviceSerial}\\Device Parameters\\

当打印到文件 （没有 USB 驱动程序存在）：

- **C:\\Windows\\System32\\假脱机\\驱动程序\\x64\\3\\MS3DPrinterDeviceConfig.xml** – 这是全局的且由切片器。

为简单起见，编辑**MS3DPrinterDeviceConfig.xml**另存为文件**管理员**如果你使用的**打印到文件**函数 （G 代码文件） 中的没有物理设备附加和编辑**StandardGCode.XML**打印到物理设备时。

现在您已准备 3D 打印到 Windows，或任何存储区中的三维生成器应用程序等应用程序或实现 Windows 本机 3D 打印的桌面应用程序中。

 

 




