---
title: 在微型驱动程序中使用资源 DLL
description: 在微型驱动程序中使用资源 DLL
keywords:
- GPD 文件 WDK Unidrv，资源 Dll
- 资源 Dll WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c7b6f576727252456046796d1834bfd78ff6388
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785979"
---
# <a name="using-resource-dlls-in-a-minidriver"></a>在微型驱动程序中使用资源 DLL





通常情况下，打印机驱动程序需要将此类资源用作外部存储的字体、图标和其他位图，并使用可本地化的用户界面文本字符串。 这些项的描述放置在资源 DLL 中，如 Microsoft Windows SDK 文档中所述。

若要在 Unidrv 微型驱动程序中使用资源 Dll，必须在以下任一礼节中标识资源：

-   如果使用多个资源 DLL，请使用 RESDLL 功能来识别它们。

    RESDLL 功能的示例用法如下所示：

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

    若要引用其中一个资源 Dll 中包含的资源，请使用以下格式：

    RESDLL.*ResourceOptionName*。*ResourceID*

-   如果只使用一个资源 DLL，则可以通过将值分配给 ResourceDLL 属性来识别它 \* 。

    若要引用此资源 DLL 中包含的资源，只需指定适当的资源标识符，如以下示例中所示：

    ```cpp
    *rcNameID: 288
    ```

与微型驱动程序一起使用的所有资源 Dll 都必须在打印机 INF 文件中指定。 请参阅 [安装 Unidrv 微型驱动程序](installing-a-unidrv-minidriver.md)。

在 *GPD* 文件中，将值分配到名称以 rc 开头的任何项（ \* \* 例如 rcIconID 和 rcCartridgeNameID）时，必须使用资源标识符 \* 。

此外，如果您的打印机包含硬件驻留字体，则您必须以. ufm 或 ifi 文件的形式提供这些字体的 [打印机字体说明](printer-font-descriptions.md) ，并且必须分别使用 RC \_ ufm 或 rc \_ 字体资源类型在资源 DLL 中标识这些文件。

Microsoft 提供了一个资源 DLL unires.dll，其中包含 [标准功能](standard-features.md) 和 [标准选项](standard-options.md)的字符串资源。 Microsoft 提供的 GPD 文件 stdnames. GPD 将宏符号名称分配给每个资源标识符。 这允许你按其宏名称引用这些资源，如以下示例中所示：

```cpp
*rcNameID: =LETTERSMALL_DISPLAY
```

 

 




