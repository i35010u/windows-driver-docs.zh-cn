---
title: 为设备提供图标
description: 为设备提供图标
ms.assetid: 2e3afbf6-57f6-4b83-b10a-c33d9b1c1731
keywords:
- 自动播放图标 WDK
- 自定义图标 WDK 设备安装
- 供应商图标 WDK
- 图标 WDK Shell
- Shell 图标 WDK
- 媒体插入的图标 WDK
- 无媒体插入图标 WDK
- 图标 WDK 自动播放
- 复制图标文件
ms.date: 04/30/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5fe372d91e5e809312801660fac3cecaeb66f9e1
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715264"
---
# <a name="providing-icons-for-a-device"></a>为设备提供图标

本主题介绍如何通过在驱动程序的 INF 文件中引用设备来为其提供自定义图标。 你可以根据需要提供显示在设备管理器、Windows 资源管理器或两者中的图标。

## <a name="adding-icons-for-device-manager"></a>为设备管理器添加图标

可以在 DLL 中嵌入自定义图标，或提供独立的 .ico 文件。 如果驱动程序已是 DLL 文件，则第一个选项是最简单的选项，因为它不需要复制任何其他文件。

若要将图标嵌入到 DLL 中，请使用如下所示的条目：

```inf
[<DDInstall>]
AddProperty = DeviceIconProperty

[DeviceIconProperty]
DeviceIcon,,,,"%13%\UmdfDriver.dll,-100"
```

上面的示例使用 DIRID 13 将文件复制到驱动程序存储区，这样就无需将其复制到其他位置。 该条目采用格式 `<Resource.dll>,-<IconResourceID>` ，因此100表示 DLL 的资源表中的图标的资源 ID。 有关 DIRID 13 的详细信息，请参阅 [使用通用 INF 文件](./using-a-universal-inf-file.md)。

若要引用独立的 .ico 文件，请使用如下所示的条目：


```inf
[<DDInstall>]
AddProperty = DeviceIconProperty

[DeviceIconProperty]
DeviceIcon,,,,"%13%\vendor.ico"
```

## <a name="adding-icons-for-storage-volumes-in-explorer"></a>在资源管理器中为存储卷添加图标

Shell 使用 " **图标** " 和 " **NoMediaIcons** " 注册表值在 "自动播放"、"我的电脑" 和 "文件打开" 对话框中表示设备。

若要添加这些内容，请在设备的[**Inf DDInstall 部分**](inf-ddinstall-hw-section.md)中包括一个[**inf AddReg 指令**](inf-addreg-directive.md)。 在 " **AddReg** " 部分中，指定 " **图标** " 和 " **NoMediaIcons** " 值项，如以下示例中所示：

```inf
[DDInstall.NT.HW]
AddReg = IconInformation

[IconInformation]
HKR, , Icons, 0x10000, "media-inserted-icon-file"
HKR, , NoMediaIcons, 0x10000, "no-media-inserted-icon-file"
```

然后，请包括一个 [**Inf SourceDisksFiles 部分**](inf-sourcedisksfiles-section.md) ，其中列出了图标文件和一个将它们复制到系统的对应 [**INF CopyFiles 指令**](inf-copyfiles-directive.md) 。

**图标**和**NoMediaIcons**值项存储在设备的*硬件密钥*下的**设备参数**项下。 例如， `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\<Hardware ID>\Device Parameters` 将包含如下所示的条目：

* `Icons [REG_MULTI_SZ] = %SystemRoot%\system32\icon.ico`

* `NoMediaIcons [REG_MULTI_SZ] = %SystemRoot%\system32\noicon.ico`

若要从用户模式修改 **设备参数** 密钥，请使用 [**SetupDiCreateDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdicreatedevregkeya) 或 [**SetupDiOpenDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendevregkey)。

在内核模式下，使用 [**IoOpenDeviceRegistryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)。

## <a name="resources"></a>资源

创建图标时，请遵循 [图标](/windows/win32/uxguide/vis-icons)中提供的指导原则。 这些准则介绍了如何创建具有 Windows 图形元素外观和行为的图标。