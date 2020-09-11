---
title: 创建移动包
description: 本主题提供有关创建用于在移动设备上安装示例驱动程序的包的信息。
ms.assetid: E929D80D-17BF-4079-8CF9-972020306358
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0a8f8cc5a651561a209adc5db6f25cd433f458fb
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010143"
---
# <a name="creating-a-mobile-package"></a>创建移动包

本主题提供有关创建用于在移动设备上安装示例驱动程序的包的信息。

执行以下任务来为示例驱动程序创建包。

1. 复制以下代码并将其粘贴到记事本中。

```XML
<?xml version="1.0" encoding="utf-8"?>
<!--
Copyright (c) Microsoft Corporation.  All rights reserved.
-->
<Package xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  Owner="OEMName"
  OwnerType="OEM"
  Component="Drivers"
  SubComponent="Adxl345Acc"
  ReleaseType="Production"
  xmlns="urn:Microsoft.WindowsPhone/PackageSchema.v8.00">
  <Components>
    <OSComponent>
      <Files>
        <File DestinationDir="$(runtime.drivers)\umdf" Source="$(_RELEASEDIR)\Adxl345Acc.dll" />
      </Files>

      <RegKeys>
        <RegKey KeyName="$(hklm.system)\ControlSet001\Enum\Root\umdf2\Adxl345Acc">
          <RegValue Name="ClassGUID"    Type="REG_SZ"        Value="{5175D334-C371-4806-B3BA-71FD53C9258D}"  />
          <RegValue Name="Class"        Type="REG_SZ"        Value="Sensor" />
          <RegValue Name="ConfigFlags"  Type="REG_DWORD"     Value="00000020"  />
          <RegValue Name="HardwareID"   Type="REG_MULTI_SZ"  Value="umdf2\Adxl345Acc"  />
        </RegKey>
      </RegKeys>
    </OSComponent>

    <!-- Use Phone-specific INF for security. -->
    <Driver InfSource="$(DRIVERS_FILES_PATH)\Adxl345Acc.inf">
      <Security InfSectionName="Sensor_Inst_SecurityAddReg">
          <AccessedByCapability Id="ID_CAP_SENSORS" Rights="$(GENERIC_READ)$(GENERIC_EXECUTE)" />
      </Security>
      <Reference Source="$(_RELEASEDIR)\Adxl345Acc.dll" />
    </Driver>

  </Components>

</Package>
```

>[!NOTE]
> **Security InfSectionName**元素的值必须与本主题中讨论的**AddReg**字段的值完全相同：请[查看 INX 文件](review-and-revise-the-inf-file.md)。

2. 在记事本的主菜单中，单击 " **文件** &gt; **另存为**"，然后在 " **另存为** " 对话框窗口中，使用下拉框将 " **保存类型** " 字段设置为 " **所有文件**"。 * * * *

3. 在 " **文件名** " 文本框中，键入以下内容：

*adxl345acc.pkg.xml*
4. 使用 " **另存为** " 对话框窗口顶部的 "目标" 框导航到 Microsoft Visual Studio 中的项目文件夹。 然后单击“保存”  。

按照前面的步骤创建 *adxl345acc.pkg.xml* 文件后，还可以使用 Windows 驱动程序工具包随附的 **pkggen.exe** 工具 (WDK) 来打包该文件。

如果已将 WDK 安装到默认位置，则可以在以下位置找到 **pkggen.exe** ： *%WPDKCONTENTROOT%\Tools\bin\i386*

有关如何为移动设备创建包的说明，请参阅 [包生成器的命令行参数](/windows-hardware/manufacture/mobile/command-line-arguments-for-package-generator) 。 有关更全面的介绍，请参阅 [创建 Mobile Pacakages](/previous-versions/windows/hardware/packaging/dn756642(v=vs.85)) 。

## <a name="related-topics"></a>相关主题

[创建移动包](/previous-versions/windows/hardware/packaging/dn756642(v=vs.85))

[查看 INX 文件](review-and-revise-the-inf-file.md)

[包生成器的命令行参数](/windows-hardware/manufacture/mobile/command-line-arguments-for-package-generator)