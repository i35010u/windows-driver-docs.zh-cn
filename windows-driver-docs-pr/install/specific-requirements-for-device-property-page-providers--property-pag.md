---
title: 属性页扩展 Dll 的要求
description: 设备属性页提供程序（属性页扩展 DLL）的特定要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf54f819e0ebaac6d7ffcd9ea9e4afc1f420bc94
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820705"
---
# <a name="specific-requirements-for-device-property-page-providers-property-page-extension-dlls"></a>设备属性页提供程序（属性页扩展 DLL）的特定要求


本主题介绍如何创建和安装属性页扩展 DLL。

### <a name="creating-a-property-page-extension-dll"></a>创建属性页扩展 dll

提供自定义属性页的属性页扩展 DLL 必须处理添加属性页的请求。 此请求通过 **AddPropSheetPageProc** 回调函数发出。

作为对此请求的响应，DLL 提供有关其每个自定义属性页的信息，创建页面，并将创建的页添加到设备的动态属性页列表中。

有关如何通过属性页扩展 DLL 创建自定义设备属性页的信息，请参阅 [设备属性页提供程序的一般要求](general-requirements-for-device-property-page-providers.md)。

### <a name="installing-a-device-property-page"></a>安装设备属性页

使用[驱动程序包](driver-packages.md)的[INF 文件](overview-of-inf-files.md)中的以下指令安装属性页扩展 DLL：

1.  使用由 [**Inf *DDInstall* 部分**](inf-ddinstall-section.md)中的 [**inf AddReg 指令**](inf-addreg-directive.md)指定的 "*添加注册表" 部分*，为设备添加 **EnumPropPages32** 条目。 **EnumPropPages32** 项指定以下 [REG_SZ](/windows/desktop/SysInfo/registry-value-types)值：

    -   导出 **ExtensionPropSheetPageProc** 回调函数的 DLL 的名称。
    -   DLL 实现的 **ExtensionPropSheetPageProc** 回调函数的名称。

    下面的代码示例演示了一个 " *添加注册表" 部分* ，该部分添加了 **EnumPropPages32** 项来指定 DLL 的名称， (*MyPropProvider.dll*) 和回调函数 (*MyCallbackFunction*) ：

    ```cpp
    HKR, , EnumPropPages32, 0, "MyPropProvider.dll, MyCallbackFunction"
    ```

    **重要提示**  DLL 和回调函数的名称必须括在引号内 ( "" ) 。

     

2.  包括将属性页扩展 DLL 复制到 *% SystemRoot% \\ System32* 目录的 [**INF CopyFiles 指令**](inf-copyfiles-directive.md)。

3.  如果设备是网络适配器，则必须将 NCF_HAS_UI 指定为 [**INF DDInstall 部分**](inf-ddinstall-section.md)中的某个 **特性** 值。 此值指示适配器支持用户界面。

    有关详细信息，请参阅为 [网络适配器指定自定义属性页](../network/specifying-custom-property-pages-for-network-adapters.md)。

 

