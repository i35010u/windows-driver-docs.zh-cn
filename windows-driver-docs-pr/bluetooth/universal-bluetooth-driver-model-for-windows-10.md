---
title: Windows 10 的蓝牙通用 Windows 驱动程序模型
description: 在 Windows 10 中，所有设备的蓝牙传输驱动程序接口都已聚合，并使用通用 Windows 驱动程序模型。
ms.assetid: E65A71D3-C0D2-4E13-9E19-1E6C6C1A172E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a79ffdf57bd27a9f2d3c2b71caf2b78157f9fe84
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010007"
---
# <a name="bluetooth-universal-windows-driver-model-for-windows-10"></a>Windows 10 的蓝牙通用 Windows 驱动程序模型


在 Windows 10 中，所有设备的蓝牙传输驱动程序接口都已聚合，并使用通用 Windows 驱动程序模型。 可以编写在所有 Windows 设备平台上运行的单一驱动程序。

蓝牙音频驱动程序接口区域针对 Windows 10 划分，并允许以下两个选项：

-   可以编写适用于桌面和移动设备的新的音频通用 Windows 驱动程序。
-   现有的 Windows Phone 8.1 蓝牙音频驱动程序将在 Windows 10 移动版上运行。

## <a name="span-idhow_to_write_a_bluetooth_universal_windows_driverspanspan-idhow_to_write_a_bluetooth_universal_windows_driverspanspan-idhow_to_write_a_bluetooth_universal_windows_driverspanhow-to-write-a-bluetooth-universal-windows-driver"></a><span id="How_to_write_a_Bluetooth_Universal_Windows_driver"></span><span id="how_to_write_a_bluetooth_universal_windows_driver"></span><span id="HOW_TO_WRITE_A_BLUETOOTH_UNIVERSAL_WINDOWS_DRIVER"></span>如何编写蓝牙通用 Windows 驱动程序


若要编写蓝牙通用 Windows 驱动程序，请参阅 [使用通用 windows 驱动程序入门](/windows-hardware/drivers)，并按照使用内核模式驱动 *程序构建通用* WINDOWS 驱动程序 (KMDF) "模板中的步骤进行操作。

然后，请参阅蓝牙设计和参考部分，了解实施指南。

-   [蓝牙配置文件驱动程序](bluetooth-profile-drivers-overview.md)
-   [蓝牙设备参考](https://msdn.microsoft.com/library/windows/hardware/ff536585)

 

