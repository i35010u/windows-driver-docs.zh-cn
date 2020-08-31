---
description: Windows 10 S 模式驱动程序要求
title: Windows 10 S 模式驱动程序要求
ms.date: 05/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1a4f895066c90695d0d57fcf202a4aff44df953
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095113"
---
# <a name="windows-10-in-s-mode-driver-requirements"></a>Windows 10 S 模式驱动程序要求

本部分介绍 Windows 10 中的驱动程序安装要求和阻止组件。  

## <a name="driver-requirements"></a>驱动程序要求

若要在 S 模式下安装 Windows 10，驱动程序包必须满足以下要求：

-   驱动程序包必须使用 windows[硬件开发人员中心仪表板](https://aka.ms/DevCenterPortal)中的**windows、WHQL、ELAM 或存储**证书进行数字签名。
-   伴生软件必须使用 [Microsoft Store 证书](/windows/uwp/publish/the-app-certification-process)进行签名。
-   不 \* \* \* \* 在驱动程序包中包含可提取未签名的二进制文件的 .exe、.zip、.msi 或 .cab。
-   仅使用 INF 指令安装驱动程序。
-   驱动程序未调用已 [阻止的收件箱组件](#blocked-inbox-components)。
-   驱动程序不包括任何用户界面组件、应用程序或设置。  请改用 Microsoft Store 的通用应用程序，例如：
    *  [硬件支持应用](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)
    *  [UWP 设备应用](../devapps/meet-uwp-device-apps.md)
    *  [Centennial 应用](https://developer.microsoft.com/windows/bridges/desktop)
-   驱动程序和固件服务使用 Windows 更新，而不是更新的应用程序。

最后，我们建议尽可能使用通用 Windows 驱动程序。  有关详细信息，请参阅：

-   [通用驱动程序的入门](../develop/getting-started-with-windows-drivers.md)
-   [验证通用驱动程序](../develop/validating-windows-drivers.md)

## <a name="installation"></a>安装

* 如果在仪表板中提交驱动程序时选中符合性复选框，则驱动程序将同时传递到 Windows 10 （在 S 模式下）和 Windows 10 的桌面版本（具有相同的硬件 ID）。 有关这些仪表板选项的详细信息，请参阅 [将驱动程序发布到 Windows 更新](../dashboard/publish-a-driver-to-windows-update.md)。
* 如果 Windows 10 在 S 模式下需要不同的驱动程序包，而 Windows 10 的桌面版本面向相同的 HWID，请在[INF 版本部分](./inf-version-section.md)为面向 Windows 10 桌面版的包设置较大的**DriverVer**条目。  例如，你可以将的 **DriverVer** 设置 `05/24/2019,10.0.1.0` 为面向 windows 10 （在 S 模式下）和面向 `05/24/2019,10.1.1.0` windows 10 的桌面版本的包。

## <a name="troubleshooting-installation"></a>排查安装问题

如果针对基本 INF 和扩展 INF 以 S 模式提供 Windows 10，但仅在桌面版本的 Windows 10 上安装扩展 INF，则已安装的驱动程序的级别较高，或者基本驱动程序未以正确的目标发布。   (子可能) 不同。    检查并比较基本驱动程序和扩展驱动程序的发货标签。

## <a name="blocked-inbox-components"></a>阻止的收件箱组件

以下组件被阻止在 Windows 10 S 上执行：

-   bash.exe
-   cdb.exe
-   cmd.exe
-   cscript.exe
-   csi.exe
-   dnx.exe
-   fsi.exe
-   hh.exe
-   Windows 10 infdefaultinstall.exe (新添加版本 1709) 
-   kd.exe
-   lxssmanager.exe
-   msbuild.exe
-   mshta.exe
-   ntsd.exe
-   powershell.exe
-   powershell_ise.exe
-   rcsi.exe
-   reg.exe
-   regedit.exe  
-   regedt32.exe
-   regini.exe
-   syskey.exe
-   wbemtest.exe
-   windbg.exe
-   wmic.exe
-   wscript.exe
-   wsl.exe

> [!接下来] 若要确保 Windows 应用在 S 模式下运行 Windows 10 的设备上正常运行，请查看应用的 [测试指南](/windows/uwp/porting/desktop-to-uwp-test-windows-s) 。