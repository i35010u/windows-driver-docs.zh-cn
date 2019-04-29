---
title: 在微型驱动程序中使用资源 DLL
description: 在微型驱动程序中使用资源 DLL
ms.assetid: b63c48bb-3321-45e0-b37c-a9612a95cc24
keywords:
- GPD 文件 WDK Unidrv，资源 Dll
- 资源 Dll WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35f74e692a08aa71c20bc6977a874b392a9b5c9a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387116"
---
# <a name="using-resource-dlls-in-a-minidriver"></a>在微型驱动程序中使用资源 DLL





通常情况下，打印机驱动程序需要从外部存储的字体、 图标和其他位图和可本地化的用户界面文本字符串作为此类资源的使用。 Microsoft Windows SDK 文档中所述，这些项的描述被放在资源 DLL。

若要使用资源 Dll 中 Unidrv 微型驱动程序，必须标识以下方式之一中的资源：

-   如果使用多个资源 DLL，确定它们使用 RESDLL 功能。

    RESDLL 功能的用法示例如下所示：

    ```cpp
    *Feature: RESDLL
    {
        *Option: FirstRes
        {*Name: "MyFirstRes.dll"}
        *Option: SecondRes
        {*Name: "MySecondRes.dll"}
        *Option: ThirdRes
        {*Name: "MyThirdRes.dll"}
    }
    ```

    若要引用一个这些资源 Dll 中包含的资源，请使用以下格式：

    RESDLL。*ResourceOptionName*。*资源 Id*

-   如果使用的一个资源 DLL，您可以通过将分配到的值来识别它\*项 ResourceDLL 属性。

    若要引用此资源 DLL 中包含的资源，只需指定适当的资源标识符，如下面的示例中所示：

    ```cpp
    *rcNameID: 288
    ```

必须在打印机 INF 文件中指定所有资源 Dll 与微型驱动程序一起使用。 请参阅[安装 Unidrv 微型驱动程序](installing-a-unidrv-minidriver.md)。

内*GPD*文件中，资源将值分配到任何项的名称开头时，必须使用标识符\*rc，如\*rcIconID 和\*rcCartridgeNameID，例如。

此外，如果您的打印机包含驻留在硬件中的字体，则必须提供[打印机字体说明](printer-font-descriptions.md).ufm 或.ifi 文件和你的窗体中的这些字体必须标识资源 DLL 中的这些文件，对于使用 RC\_UFM 或 RC\_字体资源类型，分别。

Microsoft 提供的一个资源 DLL，unires.dll，其中包含字符串资源的[标准功能](standard-features.md)并[标准选项](standard-options.md)。 Microsoft 提供 GPD 文件、 stdnames.gpd，宏符号名称添加到每个资源标识符分配。 这可以引用这些资源通过宏名称，如下面的示例中所示：

```cpp
*rcNameID: =LETTERSMALL_DISPLAY
```

 

 




