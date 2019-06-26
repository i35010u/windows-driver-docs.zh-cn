---
title: 属性页扩展 Dll 的要求
description: 设备属性页提供程序（属性页扩展 DLL）的特定要求
ms.assetid: bc48d848-a216-442e-97ca-f990f8d243ac
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2bb049acf85ad490d152ea43e38f750cadd6f2b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385890"
---
# <a name="specific-requirements-for-device-property-page-providers-property-page-extension-dlls"></a>设备属性页提供程序（属性页扩展 DLL）的特定要求


本主题如何创建和安装属性页面扩展 DLL。

### <a name="creating-a-property-page-extension-dll"></a>创建属性页扩展 dll

属性页扩展 DLL 提供自定义属性页必须处理请求，以便添加属性页。 通过发出此请求**AddPropSheetPageProc**回调函数。

以响应此请求，DLL 提供了有关每个自定义属性页的信息、 创建页，并将已创建的页添加到设备的动态属性页的列表。

有关如何创建自定义设备属性页的属性页面扩展 DLL 的信息，请参阅[设备属性页提供程序的常规要求](general-requirements-for-device-property-page-providers.md)。

### <a name="installing-a-device-property-page"></a>安装设备属性页

使用中的以下指令安装 DLL 的属性页扩展[INF 文件](overview-of-inf-files.md)的[驱动程序包](driver-packages.md):

1.  使用*添加注册表部分*，这由指定[ **INF AddReg 指令**](inf-addreg-directive.md)中[ **INF *DDInstall*一节**](inf-ddinstall-section.md)，以添加**EnumPropPages32**的设备条目。 **EnumPropPages32**项指定以下[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)值：

    -   将导出的 DLL 的名称**ExtensionPropSheetPageProc**回调函数。
    -   名称**ExtensionPropSheetPageProc**由 DLL 实现回调函数。

    下面的代码示例演示*添加注册表部分*，它将**EnumPropPages32**指定的 DLL 的名称的条目 (*MyPropProvider.dll*) 和回调函数 (*MyCallbackFunction*):

    ```cpp
    HKR, , EnumPropPages32, 0, "MyPropProvider.dll, MyCallbackFunction"
    ```

    **重要**  DLL 和回调函数名称必须一起用引号 ("")。

     

2.  包括[ **INF CopyFiles 指令**](inf-copyfiles-directive.md) ，将属性页扩展 DLL 复制到 *%systemroot%\\System32*目录。

3.  如果该设备是网络适配器，则必须作为一个指定 NCF_HAS_UI**特征**中的值[ **INF DDInstall 部分**](inf-ddinstall-section.md)。 此值指示适配器支持用户界面。

    有关详细信息，请参阅[的自定义属性页指定网络适配器](https://docs.microsoft.com/windows-hardware/drivers/network/specifying-custom-property-pages-for-network-adapters)。

 

 





