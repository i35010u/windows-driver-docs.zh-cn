---
title: 创建基元驱动程序
description: 通过基元驱动程序处理和管理使用基于 INF 的安装但不一定绑定到特定硬件设备的软件。
ms.date: 04/16/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: f94196f43c400ebd8d73a8a21f075f68219ae3d7
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065202"
---
# <a name="creating-a-new-primitive-driver"></a>创建新的基元驱动程序

通过基元驱动程序处理和管理使用基于 INF 的安装但不一定绑定到特定硬件设备的软件。

## <a name="background-and-benefits-of-primitive-drivers"></a>基元驱动程序的背景知识和优势

在 Windows 10 版本 1903 之前，使用基于 INF 的安装但不一定绑定到特定硬件设备的某些类型的软件不完全受 OS 的支持。 尽管这些软件片段使用 INF 文件作为安装清单，但 OS 不能直接认识到这种情况，因此并非原生即可支持处理这些软件。

由于这些软件片段未绑定到硬件设备，因此，无论硬件是什么，它们都会安装在整个系统上。 因此，在升级 OS 时，不保证正确安装、卸载或处理这些软件片段。

为了提高可靠性并保证此类软件的正确行为（尤其是在 OS 升级和重置方案期间），从 Windows 10 版本 1903 开始，即插即用平台现在会将此类软件包作为顶级实体进行处理和管理。

利用这种新平台支持的软件类型称为“基元驱动程序”。 基元驱动程序继续使用基于 INF 的安装，底层平台利用[驱动程序存储](../install/driver-store.md)来跟踪所有相关文件。

然后，底层即插即用平台在 OS 升级时，可正常安装、卸载和维护驱动程序状态。

从概念上讲，将以不同的方式管理这些 INF。 以前，\[DefaultInstall\]（往往是 \[DefaultUninstall\]）由 [SetupAPI](../install/setupapi.md) 以类似于脚本的方式进行处理，其中，INF 用作清单，[SetupAPI](../install/setupapi.md) 代表调用方执行相关节中的指令。

撤消更改（以执行卸载）需要指定一个 INF 节，该节执行的指令集与安装 (installation) 节相反。 但是，利用基元驱动程序的 INF 不需要卸载 (uninstallation) 节。

基元驱动程序使用的安装和卸载 API 与设备驱动程序相同，其中，卸载 API 执行的操作集与安装操作相反，安装和卸载驱动程序包的操作会处理这些节。

## <a name="inf-requirements-to-access-primitive-driver-functionality"></a>访问基元驱动程序功能所要满足的 INF 要求

* 与 PnP 驱动程序一样，**Version** 节必须完整。

  * 必须填写 **Provider** 指令。

  * 必须填写 **Class** 指令。

  * 必须填写 **ClassGuid** 指令。

* 驱动程序必须[符合 DCH](dch-principles-best-practices.md)。

* 不能有任何 \[Manufacturer\] 节存在。

* \[DefaultInstall\] 节中的体系结构必须经过修饰，不能有任何未经修饰的版本存在。

  * **正确：** \[DefaultInstall.amd64\]

  * **错误：** \[DefaultInstall\]

* \[DefaultUninstall\] 可以不在 INF 中（有关例外情况，请参阅[传统兼容性](#legacy-compatibility)）。

## <a name="primitive-drivers-targeting-only-windows-10-version-1903-and-later"></a>仅面向 Windows 10 版本 1903 和更高版本的基元驱动程序

仅面向 Windows 10 版本 1903 和更高版本的基元驱动程序应使用 [DiInstallDriver](/windows/desktop/api/newdev/nf-newdev-diinstalldriverw) 和 [DiUninstallDriver](/windows/desktop/api/newdev/nf-newdev-diuninstalldriverw) 在驱动程序存储中正确安装和卸载其软件。

驱动程序还应使用 Dirid 13 将驱动程序存储正确指定为所需的安装目标。 有关 Dirid 的详细信息，请参阅[使用 Dirid](../install/using-dirids.md)。

## <a name="legacy-compatibility"></a>传统兼容性

尽管 \[DefaultUninstall\] 在基元驱动程序中受到禁止，但为了实现与下层 OS 的兼容，行业允许一种例外情况。 Windows 引入了一个 INF 指令，可使支持基元驱动程序的 OS 版本忽略 \[DefaultUninstall\] 节。 如果驱动程序包需要支持下层 OS 版本，请包含以下语法，以确保平台适当处理这种情况：

```INF
[DefaultUninstall.NTamd64]
LegacyUninstall=1
```

\[DefaultInstall\] 和 \[DefaultUninstall\] 节中的**体系结构仍必须经过修饰**；但是，如果包含 `LegacyUninstall=1`，则 Windows 会忽略 \[DefaultUninstall\] 节（在 Windows 10 版本 1903 和更高版本中）。 这样，就可以在 INF 中包含该节，从而可以在下层的传统安装/卸载应用程序中使用该节来卸载基元驱动程序包。

从 Windows 10 版本 1903 开始，如果将经过体系结构修饰的 \[DefaultInstall\] 或 \[DefaultUninstall\] 节传入 setupapi.dll 中的 [InstallHInfSection](/windows/desktop/api/setupapi/nf-setupapi-installhinfsectionw) API，则会检查驱动程序包，以确定它是否支持基元驱动程序功能。 如果它不支持基元驱动程序功能，则不会以传统方式处理指定的节，而是适当地将 INF 传递给 [DiInstallDriver](/windows/desktop/api/newdev/nf-newdev-diinstalldrivera) 或 [DiUninstallDriver](/windows/desktop/api/newdev/nf-newdev-diuninstalldriverw)。 这样，单个安装程序就可以在兼容的 OS 版本中使用基元驱动程序，并保留以往 OS 版本的支持。

## <a name="converting-from-a-device-driver-inf"></a>从设备驱动程序 INF 进行转换

将使用 \[Manufacturer\] 的 INF 转换为使用 \[DefaultInstall\] 的 INF 需要对 INF 进行少量更改。 与 \[Manufacturer\] 节不同，\[DefaultInstall\] 节是入口点和 install 节。 这是在概念上将 \[Manufacturer\] 节、\[Models\] 节和 \[DDInstall\] 节合并为一个节。

考虑一下以下设备驱动程序 INF：

```ini
[Manufacturer]
%Company% = Driver, NTx86, NTamd64

[Driver.NTx86]
%DeviceDesc% = InstallSection_32,

[Driver.NTamd64]
%DeviceDesc% = InstallSection_64,

[InstallSection_64]
CopyFiles = MyCopyFiles_64
AddReg = MyAddReg

[InstallSection_64.Services]
AddService = MyService,, MyService_Install

[InstallSection_32]
CopyFiles = MyCopyFiles_x86
AddReg = MyAddReg

[InstallSection_32.Services]
AddService = MyService,, MyService_Install
```

此 INF 会在 [InfVerif](../devtest/infverif.md) 中收到 1297 错误，因为它不会在任何硬件上安装。 此 INF 可转换为基于 \[DefaultInstall\] 的 INF，如下所示。

```ini
[DefaultInstall.NTamd64]
CopyFiles = MyCopyFiles_64
AddReg = MyAddReg

[DefaultInstall.NTamd64.Services]
AddService = MyService,, MyService_Install

[DefaultInstall.NTx86]
CopyFiles = MyCopyFiles_x86
AddReg = MyAddReg

[DefaultInstall.NTx86.Services]
AddService = MyService,, MyService_Install
```