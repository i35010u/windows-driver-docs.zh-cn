---
title: CM_PROB_FAILED_INSTALL
description: CM_PROB_FAILED_INSTALL
keywords:
- CM_PROB_FAILED_INSTALL
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 9e18d6dab7b23517764efa09b6ed4db2cc28524e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783147"
---
# <a name="code-28---cm_prob_failed_install"></a>代码 28 - CM_PROB_FAILED_INSTALL

此设备管理器错误消息指示设备的驱动程序未安装。

## <a name="error-code"></a>错误代码

28

### <a name="display-message"></a>显示消息

"此设备的驱动程序未安装。  (代码 28) "

### <a name="recommended-resolution"></a>推荐的解决方案

请访问公司的网站，该网站用于制造设备，并查找此设备的最新驱动程序。


## <a name="for-driver-developers"></a>面向驱动程序开发人员

设备上的 [**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md) 属性应指示故障代码。

### <a name="0xc0000490---status_pnp_no_compat_drivers"></a>0xC0000490-STATUS_PNP_NO_COMPAT_DRIVERS

PnP 找不到设备的兼容驱动程序。 此失败通常称为 DNF (驱动程序) 问题。

检查相关设备的硬件 Id 和兼容 Id，并比较 INF 在 " [**模型" 部分**](inf-models-section.md)下指定) 的硬件 id (。  此外，请确保 "模型" 部分名称的 " **TargetOSVersion** " 部分适用于在其上运行的体系结构和操作系统版本。

### <a name="0xc0000491---status_pnp_driver_package_not_found"></a>0xC0000491-STATUS_PNP_DRIVER_PACKAGE_NOT_FOUND

此代码表示缺少驱动程序包依赖项。

具体而言，在设备上匹配的 **inf 使用 "** [inf DDInstall" 部分](inf-ddinstall-section.md) 中的条目来指定在此版本的 Windows 中不存在的 Microsoft 提供的 INF。

### <a name="0xc0000492---status_pnp_driver_configuration_not_found"></a>0xC0000492-STATUS_PNP_DRIVER_CONFIGURATION_NOT_FOUND

此代码还指示缺少驱动程序包依赖项。

在这种情况下，在设备上匹配的 INF **使用** [inf DDInstall 部分](inf-ddinstall-section.md) 中的条目来指定 **包含** 指令所引用的任何由 Microsoft 提供的 INF 中不存在的部分。

### <a name="0xc0000494---status_pnp_function_driver_required"></a>0xC0000494-STATUS_PNP_FUNCTION_DRIVER_REQUIRED

当 INF 未指定关联的函数驱动程序服务时，将发生此错误。

验证：

1. 正在安装的设备的 INF 文件包含 [**AddService 指令**](inf-addservice-directive.md) ，该指令使用标志 SPSVCINST_ASSOCSERVICE (0x00000002) 设置关联的服务或函数驱动程序。
2. INF 文件指定 [Inf DDInstall 部分](inf-ddinstall-section.md)中的 "**包括**" 或 "**需要**" 条目，该部分引用系统提供的驱动程序，进而在设备上设置关联的服务。

### <a name="upgrade-to-windows-10"></a>升级到 Windows 10

升级之前，设备有一个驱动程序，并且工作正常。 升级之后，会显示代码28。 这通常是因为从迁移中排除了驱动程序包。
