---
title: 创建自定义属性页
description: 创建自定义属性页
ms.assetid: 2481450f-ebb2-40e3-8a42-eabaecc1c7e4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b10b698792ad0d2f6c4770e639439b30fc42a831
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095609"
---
# <a name="creating-custom-property-pages"></a>创建自定义属性页


当 [设备属性页提供程序](types-of-device-property-page-providers.md) 处理为其设备或设备类创建属性页的请求时，提供程序应执行以下步骤：

1.  调用 [**SetupDiGetClassInstallParams**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassinstallparamsa) 以获取设备的当前类安装参数。 例如：

    ```cpp
    SP_ADDPROPERTYPAGE_DATA AddPropertyPageData;
    :
    ZeroMemory(&AddPropertyPageData, sizeof(SP_ADDPROPERTYPAGE_DATA));
    AddPropertyPageData.ClassInstallHeader.cbSize = sizeof(SP_CLASSINSTALL_HEADER);

    if (SetupDiGetClassInstallParams(DeviceInfoSet, DeviceInfoData,
         (PSP_CLASSINSTALL_HEADER)&AddPropertyPageData,
         sizeof(SP_ADDPROPERTYPAGE_DATA), NULL )) {
    ...
    ```

    在此示例中，代码零初始化了设备的安装参数将返回到的结构，并根据**SetupDiGetClassInstallParams**的要求，在**cbSize**字段中设置类安装标头的大小。 Class install 标头是每个类安装参数结构的第一个成员。

2.  使用如下所示的语句，确保尚未满足设备的动态页面的最大数量：

    ```cpp
    if (AddPropertyPageData.NumDynamicPages < 
        MAX_INSTALLWIZARD_DYNAPAGES)
     ...
    ```

    如果测试失败，请不要初始化或创建页面。 而是返回 NO_ERROR。

3.  分配用于保存任何特定于设备的数据的内存，稍后在对话框过程中将需要这些数据，并将该内存初始化为数据。 当销毁属性页时，提供程序必须在属性页回调中释放此内存。

    对于作为[共同安装](writing-a-co-installer.md)程序的提供程序，此设备特定的数据必须包括与[**DIF_ADDPROPERTYPAGE_ADVANCED**](./dif-addpropertypage-advanced.md)设备安装函数 (DIF) 代码一起传递的*DeviceInfoSet*和*DeviceInfoData* 。

    例如，属性页提供程序可以定义并使用结构，如以下示例中所示：

    ```cpp
    typedef struct _TEST_PROP_PAGE_DATA {
        HDEVINFO DeviceInfoSet;
        PSP_DEVINFO_DATA DeviceInfoData;
    } TEST_PROP_PAGE_DATA, *PTEST_PROP_PAGE_DATA;
    ...
    PTEST_PROP_PAGE_DATA     pMyPropPageData;
    ...
    pMyPropPageData = HeapAlloc(GetProcessHeap(), 0, sizeof(TESTPROP_PAGE_DATA));
    ```

4.  使用有关自定义属性页的信息初始化 PROPSHEETPAGE 结构：

    -   在 **dwFlags**中，设置自定义属性页所需的 PSP_USECALLBACK 标志和任何其他标志。 PSP_USECALLBACK 标志指示已提供回调函数。
    -   在 **pfnCallback**中，设置指向属性页的回调函数的指针。 在回调中处理 PSPCB_RELEASE 消息，并释放在步骤3中分配的内存。
    -   在 **pfnDlgProc**中，为属性页设置指向对话框过程的指针。
    -   在 **lParam**中，将指针传递到在步骤3中分配和初始化的内存区域。
    -   将其他成员设置为适用于自定义属性页。 有关 PROPSHEETPAGE 结构的详细信息，请参阅 Microsoft Windows SDK 文档。

5.  调用 **CreatePropertySheetPage** 创建新页。

6.  将新页面添加到类安装参数的 **DynamicPages** 成员中的动态属性页面列表，并递增 **NumDynamicPages** 成员。

7.  对于其他每个自定义属性页，重复步骤2到6。

8.  调用 [**SetupDiSetClassInstallParams**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassinstallparamsa) 以设置新的类安装参数，其中包括更新的属性页结构。

9.  返回 NO_ERROR。

Windows 会将新创建的属性页添加到设备的属性表中，设备管理器使 Microsoft Win32 API 调用来创建工作表。 显示属性页时，系统将调用 PROPSHEETPAGE 结构中指定的对话框过程。

 

