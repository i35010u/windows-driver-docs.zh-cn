---
title: 加载测试签名的代码
description: 介绍如何启用加载测试签名驱动程序使用 BCDEdit 工具的 TESTSIGNING 选项
ms.assetid: 4898595e-20c9-4607-aad7-792f7d1074e4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe7534761cda1bb838dded2a94f445cf373ada54
ms.sourcegitcommit: 780c4086ed59331b96bb4f6b5939cf25b9608aed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/13/2019
ms.locfileid: "65561694"
---
# <a name="enable-loading-of-test-signed-drivers"></a>启用加载的测试签名驱动程序

默认情况下，Windows 不会加载测试签名的内核模式驱动程序。 若要更改此行为并启用测试签名的驱动程序加载，请使用启动配置数据编辑器，BCDEdit.exe，若要启用或禁用 TESTSIGNING，启动配置选项。 必须具有管理员权限才能启用此选项。

> [!Note]
> 对于 64 位版本的 Windows Vista 和更高版本的 Windows，内核模式代码签名策略要求所有内核模式代码都具有数字签名。 但是，在大多数情况下，未签名的驱动程序可以安装并加载 32 位版本的 Windows Vista 和更高版本的 Windows 上。 有关详细信息，请参阅[驱动程序签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)。


## <a name="administrator-rights-required"></a>所需的管理员权限

若要使用 BCDEdit，必须是系统上的 Administrators 组的成员，并从提升的命令提示符运行命令。 若要打开提升的命令提示符窗口，键入**cmd**在 Windows 任务栏中的搜索框中，右键单击**命令提示符**在搜索结果中，然后选择**以管理员身份运行**.

> [!Warning]
> 若要使用 BCDEdit 修改引导配置数据，需要管理权限。 通过使用更改某些启动项选项**BCDEdit /set**可能导致您的计算机无法运行。 或者，使用系统配置实用程序 (MSConfig.exe) 更改启动设置。


## <a name="enable-or-disable-use-of-test-signed-code"></a>启用或禁用使用测试签名的代码

运行 BCDEdit 命令行来启用或禁用的加载测试签名的代码。 要使更改生效，是否启用或禁用选项，必须重新启动计算机后更改配置。

> [!Note]
> 设置 BCDEdit 选项之前，您可能需要禁用或暂停 BitLocker 和安全启动的计算机上。

若要启用测试签名的代码，请使用以下 BCDEdit 命令行：

```cpp
Bcdedit.exe -set TESTSIGNING ON
```

若要禁用的测试签名的代码使用，请使用以下 BCDEdit 命令行：

```cpp
Bcdedit.exe -set TESTSIGNING OFF
```

下图显示了使用 BCDEdit 命令行启用测试签名的结果。

![使用 testsigning，启动配置选项的结果的屏幕截图](images/driver-signing-enable-vista-test-signing.png)


## <a name="behavior-of-windows-when-loading-test-signed-code-is-enabled"></a>启用 Windows 加载测试签名代码时的行为

启用加载测试签名的代码后，Windows 将执行以下操作：

-   显示以提醒用户系统已启用测试签名在桌面的左下角中的水印文本"测试模式"。

-   操作系统加载程序和内核加载任何证书签名的驱动程序。 不需要链接到受信任的根证书颁发机构证书验证。 但是，每个驱动程序图像文件必须具有数字签名。
