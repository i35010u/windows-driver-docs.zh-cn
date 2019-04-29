---
title: 指定网络适配器的自定义属性页
description: 指定网络适配器的自定义属性页
ms.assetid: c9d54e9b-3d11-46d1-9c24-86a802c64a7a
keywords:
- 添加注册表部分 WDK 网络连接、 自定义属性页
- 自定义属性页 WDK 网络
- 属性页 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5926451cfcc2528c669ce986f4d47640ebaa9e1d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385447"
---
# <a name="specifying-custom-property-pages-for-network-adapters"></a>指定网络适配器的自定义属性页





如果**高级**属性页并不适用于显示网络组件 （适配器） 的配置选择，您可以创建一个或多个自定义属性页。

**若要创建自定义属性页**

1.  创建 Microsoft Win32 属性页。 然后，创建属性表扩展插件提供的 DLL *AddPropSheetPageProc*并*ExtensionPropSheetPageProc*回调函数。 有关详细信息，请参阅 Windows 2000 平台 SDK。

2.  使用*添加注册表部分*引用**DDInstall**部分，了解要添加的适配器**EnumPropPages32**密钥与该适配器的实例键。 **EnumPropPages32**密钥都有两个 REG\_SZ 值： 将导出的 DLL 的名称*ExtensionPropSheetPageProc*函数和名称*ExtensionPropSheetPageProc*函数。 以下是一种*添加注册表部分*，它将**EnumPropPages32**密钥：

    ```INF
    HKR, EnumPropPages32, 0, "DLL name, ExtensionPropSheetPageProc function name"
    ```

3.  在适配器的 INF 文件，包括**CopyFiles**部分中，将属性表扩展 DLL 复制到 Windows\\System32 目录。 有关详细信息**CopyFiles**部分中，请参阅[INF 文件的部分和指令](https://msdn.microsoft.com/library/windows/hardware/ff547433)。

4.  在中**DDInstall**部分对于适配器，指定 NCF\_HAS\_作为一个 UI**特征**值以指示适配器支持用户界面。 有关详细信息，请参阅[DDInstall 部分](ddinstall-section-in-a-network-inf-file.md)。

5.  用户将变更应用到属性页后，属性表扩展 DLL 必须着：
    -   调用**SetupDiGetDeviceInstallParams**
    -   设置 DI\_FLAGSEX\_PROPCHANGE\_挂起中 SP 标志\_DEVINSTALL\_PARAMS 结构提供的**SetupDiGetDeviceInstallParams**
    -   将传递更新的 SP\_DEVINSTALL\_结构 PARAMS **SetupDiSetDeviceInstallParams**。

        这会重新加载该驱动程序，以便它可以读取已更改的参数值。

 

 





