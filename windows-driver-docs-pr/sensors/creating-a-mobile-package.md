---
title: 创建移动包
description: 本主题提供有关创建移动设备上安装的示例驱动程序的包的信息。
ms.assetid: E929D80D-17BF-4079-8CF9-972020306358
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: a5badee09435dfa13f974503b7f5f1946b4e1797
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567032"
---
# <a name="creating-a-mobile-package"></a>创建移动包


本主题提供有关创建移动设备上安装的示例驱动程序的包的信息。

执行以下任务来创建的示例驱动程序的包。

1. 将以下代码复制并粘贴到记事本。

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
> 值**安全 InfSectionName**元素必须完全相同的值**AddReg**本主题中讨论的字段：[查看 INX 文件](review-and-revise-the-inf-file.md)。

 

2. 在记事本中主菜单中，单击**文件** &gt; **另存为**，然后在**另存为**对话框窗口中，使用下拉列表框设置**另存为类型**字段**的所有文件**。 * * *

3. 在中**文件名**文字框中，键入以下内容：

*adxl345acc.pkg.xml*
4. 使用目标框的顶部**另存为**对话框窗口中导航到 Microsoft Visual Studio 中的项目文件夹。 然后单击**保存**。

在创建后*adxl345acc.pkg.xml*文件中前面所示的步骤，还可以使用**pkggen.exe**已包含使用 Windows Driver Kit (WDK)，若要打包该文件的工具。

如果您安装 WDK 到默认位置，则可以找到**pkggen.exe**在以下位置：

*%Systemroot%\\Program Files (x86)\\Windows 工具包\\10\\工具\\bin\\i386*指[运行 pkggen.exe 工具](https://msdn.microsoft.com/windows/hardware/dn756642.aspx#run-pkg)，为若要了解如何创建你的移动设备的包。 并查看[创建移动包](https://msdn.microsoft.com/windows/hardware/dn756642.aspx)有关的更全面介绍。

## <a name="related-topics"></a>相关主题
[创建移动包](https://msdn.microsoft.com/windows/hardware/dn756642.aspx)
[查看 INX 文件](review-and-revise-the-inf-file.md)
[运行 pkggen.exe 工具](https://msdn.microsoft.com/windows/hardware/dn756642.aspx#run-pkg)



