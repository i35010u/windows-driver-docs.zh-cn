---
title: 查看 INX 文件
description: 本主题演示如何修改示例传感器驱动程序，以使其适用于在目标设备上安装传感器驱动程序的 INF 文件。
ms.assetid: 1D326C5F-5B69-4C5C-AE52-14153DF964E9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab3c989c935fb290dde31c22eb58374aa147ad4d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358761"
---
# <a name="review-the-inx-file"></a>查看 INX 文件


本主题演示如何修改示例传感器驱动程序，以使其适用于在目标设备上安装传感器驱动程序的 INF 文件。

Windows 使用安装程序安装设备驱动程序的过程的一部分的信息文件 （也称为 INF 文件）。 已生成为示例传感器驱动程序的 INF 文件*ADXL345Acc.inf*。 此文件包含安装加速感应器传感器驱动程序时，将使用 Shark Cove 上的 Windows 安装的信息。

如果在 Microsoft Visual Studio 中创建一个驱动程序项目，首先生成 INX 文件。 当您修改此泛型 INX 文件并生成您的驱动程序时，生成过程将 INX 文件转换为将用于安装驱动程序的 INF 文件。 然后构建您的驱动程序，以确保生成过程生成可用于安装传感器驱动程序的 INF 文件的工作完成以下步骤在方式。

## <a name="review-the-adxl345accinx-file"></a>查看 ADXL345Acc.inx 文件


尽管必须检查整个 INX 文件，但这些步骤将指出两个重要部分。

1. 单击*ADXL345Acc.inx*文件将其打开，并查找\[版本\]附近文件开头部分。
   ```cpp
   [Version]
   Class       = Sensor
   ClassGuid   = {5175D334-C371-4806-B3BA-71FD53C9258D}
   ```

请注意，设置为"传感器"和相应的 GUID 的设备类提供。 关于设备类 GUID 用于 Windows 的详细信息，请参阅[系统定义设备安装程序类可用于供应商](https://docs.microsoft.com/windows-hardware/drivers/install/system-defined-device-setup-classes-available-to-vendors)。

2. 查找\[ADXL345Acc\_Device.NT$ARCH$\]部分。
   ```cpp
   [ADXL345Acc_Device.NT$ARCH$]
   ; DisplayName       Section          DeviceId
   ; -----------       -------          --------
   %ADXL345Acc_DevDesc% = ADXL345Acc_Inst, ACPI\ADXL345Acc
   ```

请务必注意，在以上片段中 （在此情况下，"ADXL345Acc"） 的 DeviceId 的值对应于用于更新的硬件信息文件称为辅助系统描述表 (SSDT) 的设备名称。

如果不在移动设备上安装示例传感器驱动程序，然后后更新相关的通用文件，包括 INX 文件，请参阅[生成传感器驱动程序](build-the-sensor-driver.md)，若要了解如何构建 Visual Studio 中的驱动程序。 生成过程生成传感器驱动程序文件，其中包括 Shark Cove 上安装该驱动程序时，Windows 将使用的 INF 文件。

## <a name="inf-file-for-a-mobile-device"></a>移动设备的 INF 文件


如果你将移动设备，而不 Shark Cove，用作目标设备进行测试的示例驱动程序，然后执行以下额外任务更新 INF 文件。

1. 在中*ADXL345Acc.inx*文件中，找到\[ADXL345Acc\_Inst.NT.HW\]部分，并请注意，为空。

**重要**  不要更新你的 INF 文件以用于移动设备上，则您必须将保留\[ADXL345Acc\_Inst.NT.HW\]部分为空。 在这种情况下，跳过此部分中的任务，并转到[生成传感器驱动程序](build-the-sensor-driver.md)主题。

 

2. 将以下代码片段添加到空部分。

```cpp
[ADXL345Acc_Inst.NT.HW]
AddReg=Sensor_Inst_SecurityAddReg

[Sensor_Inst_SecurityAddReg]
HKR,,Security,,"D:P(A;;GA;;;BA)(A;;GA;;;SY)(A;;GA;;;S-1-5-84-0-0-0-0-0)"    ; Allow all UMDF drivers to access this driver
```

**重要**  请记下 AddReg 字段的值，因为它必须与添加到的文件，你将在下一步中更新值中的一个精确匹配。 将从前面的代码片段示例，请记下的*传感器\_Inst\_SecurityAddReg*。

 

3. [创建移动包](creating-a-mobile-package.md)在你的移动设备上安装的示例驱动程序。

## <a name="related-topics"></a>相关主题

[创建移动包](creating-a-mobile-package.md)



