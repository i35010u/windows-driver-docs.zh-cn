---
title: Windows 10 S 模式驱动程序要求
ms.date: 05/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae2b25df5609f6d7dade0de6f2bf4f8b0859d55b
ms.sourcegitcommit: fc42f2042aad57cf19fac798ff838bb064b1a4e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2019
ms.locfileid: "66223226"
---
# <a name="windows-10-in-s-mode-driver-requirements"></a>Windows 10 S 模式驱动程序要求

本部分介绍 Windows 10 S 上的驱动程序安装要求和阻止的组件  

## <a name="driver-requirements"></a>驱动程序要求

若要在 S 模式下安装在 Windows 10 上，驱动程序包必须满足以下要求：

-   驱动程序包必须使用数字签名**Windows、 WHQL、 ELAM 或应用商店**证书从[Windows 硬件开发人员中心仪表板](https://aka.ms/DevCenterPortal)。
-   附带的软件必须使用签名[Microsoft Store 证书](https://docs.microsoft.com/windows/uwp/publish/the-app-certification-process)。
-   不包括\*.exe \*.zip， \*.msi 或\*.cab 提取未签名的二进制文件的驱动程序包中。
-   驱动程序安装使用仅 INF 指令。
-   驱动程序不会调用[阻止收件箱组件](#blocked-inbox-components)。
-   驱动程序不包括任何用户界面组件、 应用或设置。  相反，例如从 Microsoft Store 中，使用通用应用程序：
    *  [硬件支持应用程序](https://docs.microsoft.com/windows-hardware/drivers/devapps/hardware-access-for-universal-windows-platform-apps)
    *  [UWP 的设备应用程序](https://docs.microsoft.com/windows-hardware/drivers/devapps/meet-uwp-device-apps)
    *  [Centennial 应用](https://developer.microsoft.com/windows/bridges/desktop)
-   驱动程序和固件服务使用 Windows 更新并不是更新程序应用。

最后，我们建议使用通用 Windows 驱动程序，在可能的情况。  有关详细信息，请参阅：

-   [开始使用通用驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)
-   [验证通用驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/validating-universal-drivers)

## <a name="installation"></a>安装

* 如果提交仪表板中的驱动程序时检查 S 法规遵从性复选框，该驱动程序传递到这两个 Windows 10 S 模式以及桌面版本的 Windows 10 的具有相同的硬件 id。 有关这些仪表板选项的详细信息，请参阅[发布到 Windows 更新的驱动程序](https://docs.microsoft.com/windows-hardware/drivers/dashboard/publish-a-driver-to-windows-update)。
* 如果不同的驱动程序包所需的 Windows 10 S 模式和面向相同 HWID 的桌面版本的 Windows 10 中，设置一个大于**DriverVer**中的条目[INF 版本部分](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)包面向桌面版本的 Windows 10。  例如，你可能会设置**DriverVer**的`05/24/2019,10.0.1.0`包在 S 模式下，面向 Windows 10 和`05/24/2019,10.1.1.0`面向 Windows 10 的桌面版本的包。

## <a name="troubleshooting-installation"></a>安装故障排除

如果你面向的 Windows 10 S 模式下基 INF 和扩展 INF，但仅在桌面版本的 Windows 10 安装 INF 的扩展，然后您已安装的驱动程序是更高级别的或未与正确的目标发布基础驱动程序运算结果。  （CHID 可能与此不同）。    检查并比较所传送的基本驱动程序和扩展驱动程序的标签。

## <a name="blocked-inbox-components"></a>已阻止收件箱组件

以下组件会阻止在 Windows 10 s： 上执行

-   bash.exe
-   cdb.exe
-   cmd.exe
-   cscript.exe
-   csi.exe
-   dnx.exe
-   fsi.exe
-   hh.exe
-   infdefaultinstall.exe （新增适用于 Windows 10，版本 1709年）
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

> [!接下来] 若要确保您的 Windows 应用程序将在 S 模式下运行 Windows 10 的设备上正常运行，请查看[测试指导](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-test-windows-s)的应用。 
