---
title: 正在加载测试签名代码
description: 介绍如何使用 TESTSIGNING 选项和 BCDEdit 工具来启用测试签名驱动程序的加载
ms.date: 02/15/2021
ms.localizationpriority: medium
ms.custom: contperf-fy21q3
ms.openlocfilehash: 5a9b0605395ef6d3df47ab6f4444c480f3942ea7
ms.sourcegitcommit: 0d17420536cdee32336cbc73e6c58c47d9b64a30
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2021
ms.locfileid: "100532354"
---
# <a name="enable-loading-of-test-signed-drivers"></a>允许加载已进行测试签名的驱动程序

默认情况下，Windows 不会加载测试签名的内核模式驱动程序。 若要更改此行为并启用要加载的测试签名驱动程序，请使用启动配置数据编辑器 BCDEdit.exe，启用或禁用 TESTSIGNING，这是一个启动配置选项。 若要启用此选项，您必须具有管理员权限。

> [!Note]
> 对于64位版本的 Windows Vista 和更高版本的 Windows，内核模式代码签名策略要求所有内核模式代码都具有数字签名。 但在大多数情况下，可以在32位版本的 Windows Vista 和更高版本的 Windows 上安装和加载未签名的驱动程序。 有关详细信息，请参阅 [驱动程序签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)。


## <a name="administrator-rights-required"></a>需要管理员权限

若要使用 BCDEdit，你必须是系统上 Administrators 组的成员，并从提升的命令提示符运行该命令。 若要打开提升的命令提示符窗口，请在 Windows 任务栏的搜索框中键入 **cmd** ，选择并按住 (或右键单击搜索结果中) **命令提示符** ，然后选择 " **以管理员身份运行**"。

> [!Warning]
> 使用 BCDEdit 修改启动配置数据需要管理权限。 使用 **BCDEdit/set** 更改某些启动项选项可能导致计算机无法操作。 作为替代方法，使用系统配置实用工具 (MSConfig.exe) 更改启动设置。


## <a name="enable-or-disable-use-of-test-signed-code"></a>启用或禁用测试签名代码的使用

运行 BCDEdit 命令行以启用或禁用测试签名代码的加载。 要使更改生效，无论是启用还是禁用该选项，都必须在更改配置后重新启动计算机。

若要启用测试签名代码，请使用以下 BCDEdit 命令行：

```cmd
:: If this command results in "The value is protected by Secure Boot policy and cannot be modified or deleted"
:: Then reboot the PC, go into BIOS settings, and disable Secure Boot. BitLocker may also affect your ability to modify this setting.
Bcdedit.exe -set TESTSIGNING ON
```

若要禁止使用测试签名代码，请使用以下 BCDEdit 命令行：

```cmd
Bcdedit.exe -set TESTSIGNING OFF
```

下图显示了使用 BCDEdit 命令行启用测试签名的结果。

![使用 testsigning 的结果的屏幕截图，启动配置选项](images/driver-signing-enable-vista-test-signing.png)


## <a name="behavior-of-windows-when-loading-test-signed-code-is-enabled"></a>启用加载测试签名代码时 Windows 的行为

在加载测试签名代码时，Windows 会执行以下操作：

-   在桌面的所有四个角显示带有文本 "Test Mode" 的水印，以提醒用户系统已启用测试签名。
    **注意**  从 Windows 7 开始，Windows 仅将此水印显示在桌面的右下角。

-   在桌面左下角显示带有文本 "Test Mode" 的水印，以提醒用户系统已启用测试签名。

-   操作系统加载程序和由任何证书签名的内核加载驱动程序。 链接到受信任的根证书颁发机构不需要证书验证。 但是，每个驱动程序图像文件必须具有数字签名。
