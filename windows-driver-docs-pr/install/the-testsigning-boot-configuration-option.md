---
title: TESTSIGNING 启动配置选项
description: TESTSIGNING 启动配置选项
ms.assetid: 4898595e-20c9-4607-aad7-792f7d1074e4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 009082b702987ab3abacfadca89f3b6e90c32ac0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565975"
---
# <a name="the-testsigning-boot-configuration-option"></a>TESTSIGNING 启动配置选项


TESTSIGNING 启动配置选项确定 Windows Vista 和更高版本的 Windows 会加载任何类型的测试签名的内核模式代码。 默认情况下，这意味着测试签名的内核模式驱动程序将不加载在 64 位版本的 Windows Vista 和更高版本的 Windows 上默认不设置此选项。

**请注意**  内核模式代码签名策略的 64 位版本的 Windows Vista 和更高版本的 Windows，要求所有内核模式代码都具有数字签名。 但是，在大多数情况下，未签名的驱动程序可以安装并加载 32 位版本的 Windows Vista 和更高版本的 Windows 上。 有关详细信息，请参阅[内核模式代码签名策略 （Windows Vista 和更高版本）](kernel-mode-code-signing-policy--windows-vista-and-later-.md)。

 

启用或禁用通过 BCDEdit 命令 TESTSIGNING 启动配置选项。 若要启用测试签名，请使用以下 BCDEdit 命令：

```cpp
Bcdedit.exe -set TESTSIGNING ON
```

若要禁用测试签名，请使用以下 BCDEdit 命令：

```cpp
Bcdedit.exe -set TESTSIGNING OFF
```

**请注意**  更改 TESTSIGNING 启动配置选项后，重新启动计算机，更改才能生效。

 

**谨慎**  使用 BCDEdit 修改 BCD 所需的管理权限。 更改某些启动项选项使用**BCDEdit /set**命令可能导致您的计算机无法运行。 或者，使用系统配置实用程序 (MSConfig.exe) 更改启动设置。

**请注意**  之前设置可能需要禁用或暂停 BitLocker 和安全启动的计算机上的 BCDEdit 选项。

 

 

若要使用 BCDEdit，必须是系统上的 Administrators 组的成员，并从提升的命令提示符运行命令。 若要打开提升的命令提示符窗口，请创建桌面快捷方式*Cmd.exe*，右键单击*Cmd.exe*快捷方式，然后选择**以管理员身份运行**。

下面的屏幕截图显示了使用 BCDEdit 命令行工具来启用测试签名的结果。

![使用 testsigning 启动配置选项的结果的屏幕截图](images/driver-signing-enable-vista-test-signing.png)

启用测试签名的 BCDEdit 选项后，Windows 将执行以下操作：

-   显示一个水印文本中的"测试模式"全部四个角的桌面，以提醒用户系统已启用测试签名。
    **请注意**  从 Windows 7 开始，Windows 仅在桌面的左下角中将显示此水印。

     

-   操作系统加载程序和内核加载任何证书签名的驱动程序。 不需要链接到受信任的根证书颁发机构证书验证。 但是，每个驱动程序图像文件必须具有数字签名。

 

 





