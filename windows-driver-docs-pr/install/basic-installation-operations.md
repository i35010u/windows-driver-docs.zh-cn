---
title: 基本安装操作
description: 基本安装操作
ms.assetid: 9bf1a3e1-6c2a-4f8c-8694-6e859a73d9a6
keywords:
- Setupapi.log 函数 WDK，基本安装操作
- 设备安装功能 WDK Setupapi.log
- 常规设置函数 WDK Setupapi.log
- SP_DEVINFO_DATA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93f71303ce6bafc870b53977eaf4fe609aa0ffa2
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095631"
---
# <a name="basic-installation-operations"></a>基本安装操作





安装程序可以使用 Setupapi.log 提供的 [常规设置功能](/previous-versions/ff544985(v=vs.85)) 和 [设备安装功能](/previous-versions/ff541299(v=vs.85)) 来执行安装操作。 这些函数允许安装程序搜索 INF 文件以查找兼容的驱动程序，通过选择对话框向用户显示驱动程序选项，以及执行实际的驱动程序安装。

大多数设备安装函数依赖于 [**SP_DEVINFO_DATA**](/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data) 结构中的信息来执行安装任务。 每个设备都与 SP_DEVINFO_DATA 结构相关联。 可以通过使用[**SetupDiGetClassDevs**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)函数检索包含特定类中所有已安装设备的[设备信息集](device-information-sets.md) (HDEVINFO) 的句柄。 可以使用 [**SetupDiCreateDeviceInfo**](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa) 函数向设备信息集添加新设备。 通过使用 [**SetupDiDestroyDeviceInfoList**](/windows/desktop/api/setupapi/nf-setupapi-setupdidestroydeviceinfolist) 函数，可以释放设备信息集中的所有 SP_DEVINFO_DATA 结构。 此函数还可释放任何可能已添加到结构中的兼容设备和类设备列表。

通过使用 [**SetupDiBuildDriverInfoList**](/windows/desktop/api/setupapi/nf-setupapi-setupdibuilddriverinfolist) 函数，你可以生成一个列表，安装程序或用户可以从该列表中选择要安装的驱动程序或设备。 **SetupDiBuildDriverInfoList** 创建一个兼容驱动程序的列表或特定类的所有设备的列表。

获得兼容驱动程序的列表后，可以通过使用 [**SetupDiSelectDevice**](/windows/desktop/api/setupapi/nf-setupapi-setupdiselectdevice) 函数提示用户从列表中进行选择。 此函数显示一个对话框，其中包含有关设备信息集中每个设备的信息。 您可以使用 [**SetupDiInstallDevice**](/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice) 函数安装所选的驱动程序。 此函数使用驱动程序的 INF 文件中的信息来创建任何所需的新注册表项、设置设备硬件的配置以及将驱动程序文件复制到相应的目录。

安装程序可能必须检查并设置要安装的设备的注册表项下的值。 可以使用 [**SetupDiCreateDevRegKey**](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya) 或 [**SetupDiOpenDevRegKey**](/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey) 函数打开设备的硬件或驱动程序密钥。

可以使用[**SetupDiInstallClass**](/windows/desktop/api/setupapi/nf-setupapi-setupdiinstallclassa)函数安装新的[设备安装程序类](./overview-of-device-setup-classes.md)。 此函数从包含 [**Inf ClassInstall32 部分**](inf-classinstall32-section.md)的 inf 文件安装新安装程序类。

可以使用 [**SetupDiRemoveDevice**](/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedevice) 函数从系统中删除设备。 此函数删除设备的注册表项，并在可能的情况下停止设备。 如果设备无法动态停止，则该函数将设置标志，最终会导致提示用户关闭系统。

 

