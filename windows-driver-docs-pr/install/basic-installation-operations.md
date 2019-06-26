---
title: 基本安装操作
description: 基本安装操作
ms.assetid: 9bf1a3e1-6c2a-4f8c-8694-6e859a73d9a6
keywords:
- 安装程序 Api 函数 WDK，基本的安装操作
- 设备安装函数 WDK SetupAPI
- 常规安装函数 WDK SetupAPI
- SP_DEVINFO_DATA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0671756fe6a075873f1296ddc07ce08d037bf99f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385638"
---
# <a name="basic-installation-operations"></a>基本安装操作





安装程序可以使用[常规安装函数](https://docs.microsoft.com/previous-versions/ff544985(v=vs.85))并[设备安装函数](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))提供的安装程序 Api 来执行安装操作。 这些函数允许安装程序搜索兼容的驱动程序，以选择对话框，通过向用户显示驱动程序选项，并执行实际的驱动程序安装的 INF 文件。

大多数设备安装函数依赖于中的信息[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)结构，以执行安装任务。 每个设备都具有 SP_DEVINFO_DATA 结构相关联。 您可以检索到的句柄 (HDEVINFO)[设备信息集](device-information-sets.md)通过使用包含特定的类中的所有已安装的设备[ **SetupDiGetClassDevs** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)函数。 可以使用[ **SetupDiCreateDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa)函数以将新设备添加到设备的信息集。 您可以使用设置的设备信息中的所有 SP_DEVINFO_DATA 结构来都释放[ **SetupDiDestroyDeviceInfoList** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidestroydeviceinfolist)函数。 此函数还释放任何兼容设备和类设备列表可能已添加到结构。

通过使用[ **SetupDiBuildDriverInfoList** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuilddriverinfolist)函数，可以生成安装程序或用户可以从中选择的驱动程序或设备以安装的列表。 **SetupDiBuildDriverInfoList**创建兼容的驱动程序的列表或特定类的所有设备的列表。

兼容的驱动程序的列表后，可以提示用户通过从列表中选择[ **SetupDiSelectDevice** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectdevice)函数。 此函数将显示一个对话框，其中包含有关设备信息集中的每个设备的信息。 可以使用来安装所选的驱动[ **SetupDiInstallDevice** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)函数。 此函数使用驱动程序的 INF 文件中的信息来创建到任何所需，若要设置的设备硬件配置，并将驱动程序文件复制到相应目录的新注册表项。

安装程序可能需要检查和设置是在要安装的设备注册表项下的值。 可以使用打开设备的硬件或驱动程序键[ **SetupDiCreateDevRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)或[ **SetupDiOpenDevRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)函数.

你可以安装新[设备安装程序类](device-setup-classes.md)通过使用[ **SetupDiInstallClass** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstallclassa)函数。 此函数将从包含一个 INF 文件安装新的安装程序类[ **INF ClassInstall32 部分**](inf-classinstall32-section.md)。

可以通过使用从系统中删除设备[ **SetupDiRemoveDevice** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedevice)函数。 此函数将删除设备的注册表项，并如有可能，使设备停止。 如果不能动态停用设备，该函数将设置最终会使系统关闭的情况下系统会提示用户的标志。

 

 





