---
title: 创建自定义属性页
description: 创建自定义属性页
ms.assetid: 2481450f-ebb2-40e3-8a42-eabaecc1c7e4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 897cf3f7d0d0e2575d37de6649b11d45476a571b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562051"
---
# <a name="creating-custom-property-pages"></a>创建自定义属性页


当[设备属性页提供程序](types-of-device-property-page-providers.md)请求来创建其设备或设备类的属性页的句柄，该提供程序应执行以下步骤：

1.  调用[ **SetupDiGetClassInstallParams** ](https://msdn.microsoft.com/library/windows/hardware/ff551083)若要获取当前类安装设备的参数。 例如：

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

    在此示例中，代码执行零初始化在其中将返回设备的安装参数，该结构并集的大小类的安装中的标头**cbSize**所需的字段**SetupDiGetClassInstallParams**。 类安装标头是安装的每个类参数结构的第一个成员。

2.  请确保，设备的动态页面的最大数目未尚未满足使用语句如下所示：

    ```cpp
    if (AddPropertyPageData.NumDynamicPages < 
        MAX_INSTALLWIZARD_DYNAPAGES)
     ...
    ```

    如果测试失败，无法初始化或创建页。 改为返回 NO_ERROR。

3.  分配内存要在其中保存任何特定于设备的数据将需要更高版本中的对话框过程并初始化此内存的数据。 销毁属性页时，提供程序必须释放此内存在其属性页回调。

    提供程序[共同安装程序](writing-a-co-installer.md)，此特定于设备的数据必须包括*DeviceInfoSet*并*DeviceInfoData*已通过但存在[ **DIF_ADDPROPERTYPAGE_ADVANCED** ](https://msdn.microsoft.com/library/windows/hardware/ff543656)设备安装函数 (DIF) 代码。

    例如，属性页提供程序可以定义并使用一种结构，如下面的示例中所示：

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

4.  初始化具有自定义属性页信息的 PROPSHEETPAGE 结构：

    -   在中**dwFlags**，设置 PSP_USECALLBACK 标志和所需的自定义属性页的任何其他标志。 PSP_USECALLBACK 标志指示已提供一个回调函数。
    -   在中**pfnCallback**，将指针设置到的属性页的回调函数。 在回调中，处理 PSPCB_RELEASE 消息并释放已分配在步骤 3 中的内存。
    -   在中**pfnDlgProc**，将指针设置到的属性页对话框过程。
    -   在中**lParam**，将指针传递给已分配和在步骤 3 中初始化的内存区域。
    -   根据自定义属性页需要设置其他成员。 请参阅有关 PROPSHEETPAGE 结构的详细信息的 Microsoft Windows SDK 文档。

5.  调用**CreatePropertySheetPage**若要创建新的页。

6.  将新页面添加到列表中的动态属性页**DynamicPages**类的成员安装参数和增量**NumDynamicPages**成员。

7.  对每个其他自定义属性页重复步骤 2 到 6。

8.  调用[ **SetupDiSetClassInstallParams** ](https://msdn.microsoft.com/library/windows/hardware/ff552122)若要设置的新类安装参数，包括更新后的属性页结构。

9.  返回 NO_ERROR。

Windows 将新创建的属性页添加到该设备的属性表和设备管理器使 Microsoft Win32 API 调用，以创建工作表。 显示属性页时，系统将调用 PROPSHEETPAGE 结构中指定的对话框过程。

 

 





