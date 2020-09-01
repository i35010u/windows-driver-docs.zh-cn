---
title: 指定网络适配器的自定义属性页
description: 指定网络适配器的自定义属性页
ms.assetid: c9d54e9b-3d11-46d1-9c24-86a802c64a7a
keywords:
- 添加-注册表-WDK 网络，自定义属性页
- 自定义属性页 WDK 网络
- 属性页 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a238eeedf3bb1ad31121c61995fb411b5162d8b0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207409"
---
# <a name="specifying-custom-property-pages-for-network-adapters"></a>指定网络适配器的自定义属性页





如果 " **高级** " 属性页不适合用于显示网络组件 (适配器) 的配置选项，则可以创建一个或多个自定义属性页。

**创建自定义属性页**

1.  创建 Microsoft Win32 属性页。 然后创建提供 *AddPropSheetPageProc* 和 *ExtensionPropSheetPageProc* 回调函数的属性表扩展 DLL。 有关详细信息，请参阅 Windows 2000 平台 SDK。

2.  使用适配器的**DDInstall**部分引用的 "*添加注册表" 部分*，将**EnumPropPages32**项添加到适配器的实例键。 **EnumPropPages32**键具有两个 REG \_ SZ 值：导出*ExtensionPropSheetPageProc*函数的 DLL 的名称和*ExtensionPropSheetPageProc*函数的名称。 下面是添加**EnumPropPages32**项的 "*添加注册表" 部分*的示例：

    ```INF
    HKR, EnumPropPages32, 0, "DLL name, ExtensionPropSheetPageProc function name"
    ```

3.  在适配器的 INF 文件中，包含将属性表扩展 DLL 复制到 Windows System32 目录的 **CopyFiles** 部分 \\ 。 有关 **CopyFiles** 部分的详细信息，请参阅 [INF 文件部分和指令](../install/index.md)。

4.  在适配器的 " **DDInstall** " 部分中，指定 \_ \_ "NCF" 将 UI 作为 **特性** 值之一，指示适配器支持用户界面。 有关详细信息，请参阅 [DDInstall 部分](ddinstall-section-in-a-network-inf-file.md)。

5.  用户将更改应用到属性页后，必须执行以下操作：
    -   调用 **SetupDiGetDeviceInstallParams**
    -   \_ \_ \_ 在 \_ \_ **SetupDiGetDeviceInstallParams**提供的 SP DEVINSTALL 参数结构中设置 DI FLAGSEX PROPCHANGE 挂起标志
    -   将更新的 SP \_ DEVINSTALL \_ PARAMS 结构传递到 **SetupDiSetDeviceInstallParams**。

        这会重新加载驱动程序，以便它可以读取更改的参数值。

 

