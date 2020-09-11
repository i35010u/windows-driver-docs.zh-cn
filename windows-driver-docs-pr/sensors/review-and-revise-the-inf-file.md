---
title: 查看 INX 文件
description: 本主题说明如何修改示例传感器驱动程序的 INF 文件，使其适合在目标设备上安装传感器驱动程序。
ms.assetid: 1D326C5F-5B69-4C5C-AE52-14153DF964E9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b48fad055516700d2ede33d9c90f728c0c22863
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010137"
---
# <a name="review-the-inx-file"></a>查看 INX 文件


本主题说明如何修改示例传感器驱动程序的 INF 文件，使其适合在目标设备上安装传感器驱动程序。

Windows 使用安装程序信息文件 (也称为 INF 文件) 作为安装设备驱动程序的过程的一部分。 为示例传感器驱动程序生成的 INF 文件为 *ADXL345Acc*。 此文件包含带 Cove 上的 Windows 安装在安装加速感应器的传感器驱动程序时将使用的信息。

在 Microsoft Visual Studio 中创建驱动程序项目时，将首先生成一个 INX 文件。 当修改此通用 INX 文件并构建驱动程序时，生成过程会将 INX 文件转换为用于安装驱动程序的 INF 文件。 在构建驱动程序之前，通过以下步骤完成工作，以确保生成过程生成可用于安装传感器驱动程序的 INF 文件。

## <a name="review-the-adxl345accinx-file"></a>查看 ADXL345Acc. inx 文件


尽管必须完全查看 INX 文件，但这些步骤将指出两个重要部分。

1. 单击 " *ADXL345Acc inx* " 文件以将其打开，并找到 \[ 文件开头附近的 "版本" \] 部分。
   ```cpp
   [Version]
   Class       = Sensor
   ClassGuid   = {5175D334-C371-4806-B3BA-71FD53C9258D}
   ```

请注意，设备类设置为 "传感器"，并提供了相应的 GUID。 有关 Windows 的设备类 GUID 的详细信息，请参阅 [供应商可用的系统定义的设备安装程序类](../install/system-defined-device-setup-classes-available-to-vendors.md)。

2. 查找 \[ ADXL345Acc \_ 设备 NT $ $ $ $ $ $ \] 。
   ```cpp
   [ADXL345Acc_Device.NT$ARCH$]
   ; DisplayName       Section          DeviceId
   ; -----------       -------          --------
   %ADXL345Acc_DevDesc% = ADXL345Acc_Inst, ACPI\ADXL345Acc
   ```

需要注意的是，在这种情况下，前面代码段中的 DeviceId 值 (，) 与用于更新 "硬件信息" 文件（称为辅助系统说明表 (SSDT) ）的设备名称相对应。

如果不是在移动设备上安装示例传感器驱动程序，则在更新相关的通用文件（包括 INX 文件）后，请参阅 [构建传感器驱动程序](build-the-sensor-driver.md)，以了解如何在 Visual Studio 中生成驱动程序。 生成过程将生成传感器驱动程序文件，包括 Windows 在带 Cove 上安装驱动程序时将使用的 INF 文件。

## <a name="inf-file-for-a-mobile-device"></a>移动设备的 INF 文件


如果你使用的是移动设备，而不是使用带 Cove 作为目标设备来测试示例驱动程序，请执行以下其他任务来更新 INF 文件。

1. 在 *ADXL345Acc* 文件中，找到 " \[ ADXL345Acc 指令" \_ \] 部分，注意它是空的。

**重要提示**   如果未更新要在移动设备上使用的 INF 文件，则必须将 \[ ADXL345Acc \_ 指令 \] 部分留空。 在这种情况下，请跳过本部分中的任务，然后转到 [生成传感器驱动程序](build-the-sensor-driver.md) 主题。

 

2. 将以下代码片段添加到空部分。

```cpp
[ADXL345Acc_Inst.NT.HW]
AddReg=Sensor_Inst_SecurityAddReg

[Sensor_Inst_SecurityAddReg]
HKR,,Security,,"D:P(A;;GA;;;BA)(A;;GA;;;SY)(A;;GA;;;S-1-5-84-0-0-0-0-0)"    ; Allow all UMDF drivers to access this driver
```

**重要提示**   记下 "AddReg" 字段的值，因为它必须与你添加到将在下一步中更新的文件的一个值完全匹配。 在前面的代码片段示例中，可以记下 *传感器 \_ 指令 \_ SecurityAddReg*。

 

3. [创建一个移动包](creating-a-mobile-package.md) ，用于在移动设备上安装示例驱动程序。

## <a name="related-topics"></a>相关主题

[创建移动包](creating-a-mobile-package.md)