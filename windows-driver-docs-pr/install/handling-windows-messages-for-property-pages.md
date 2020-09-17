---
title: 处理属性页的 Windows 消息
description: 处理属性页的 Windows 消息
ms.assetid: 4920a003-59b5-41dc-a8ee-5e034087006a
keywords:
- 设备属性页 WDK 设备安装，Windows 消息
- 属性页 WDK 设备安装，Windows 消息
- 自定义属性页 WDK 设备安装，Windows 消息
- WM_INITDIALOG
- Windows 消息 WDK 属性页
- SendDlgItemMessage
- 友好名称 WDK 属性页
- WM_NOTIFY
- PSN_APPLY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: faf1144be6b936fa741cfda311541c07c5c46dec
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716188"
---
# <a name="handling-windows-messages-for-property-pages"></a>处理属性页的 Windows 消息





当 [设备属性页提供程序](types-of-device-property-page-providers.md) 处理为其设备或设备类创建属性页的请求时，它将返回该属性页的对话框过程的地址。 对话框过程必须在获取 WM_INITDIALOG 消息时初始化属性页，并且在获取 WM_NOTIFY 消息时必须准备好处理设备属性的更改。 该过程还可以处理它可能需要的任何其他此类消息，如 Microsoft Windows SDK 文档中所述。

为了响应 WM_INITDIALOG 消息，对话框过程将在属性页中初始化信息。 此类信息可能包括一个图标，表示设备、设备的友好名称及其 PnP 设备描述。

[**SetupDiLoadClassIcon**](/windows/win32/api/setupapi/nf-setupapi-setupdiloadclassicon) 加载指定设备类的图标，并向已加载的大图标返回一个句柄，可在对 **SendDlgItemMessage**的后续调用中使用该句柄。 例如：

```cpp
if (SetupDiLoadClassIcon(
        &pTestPropPageData->DeviceInfoData->ClassGuid, &ClassIcon, 
        NULL)) {
    OldIcon = (HICON)SendDlgItemMessage(
                        hDlg, 
                        IDC_TEST_ICON,
                        STM_SETICON, (WPARAM)ClassIcon, 0);
    if (OldIcon) {
                DestroyIcon(OldIcon);
    }
}
```

可以将 ClassIcon 中返回的句柄强制转换为 SendDlgItemMessage 函数所需的 WPARAM。 在此示例中，IDC_TEST_ICON 在接收 STM_SETICON 消息的对话框中标识控件。 IDC_TEST_ICON 的值必须在提供程序中定义。 有关操作图标和位图的其他函数，请参阅 [设备安装函数](/previous-versions/ff541299(v=vs.85))。 有关 **SendDlgItemMessage**、 **DestroyIcon**和在对话框中使用图标的详细信息，请参阅 Windows SDK 文档。

除了表示设备的图标，典型的设备属性页还包括设备的描述或 "友好名称"，并显示设备属性的当前设置。 即插即用 (PnP) manager 将每台设备的 PnP 属性存储在注册表中。 属性页提供程序可以调用 [**SetupDiGetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya) 来获取任何此类属性的值。 如果在安装过程中也将设备或类特定的配置信息存储在注册表中，则属性页提供程序可以使用其他 **SetupDiXxx** 函数来提取要显示的信息。 有关详细信息，请参阅 [设备安装函数](/previous-versions/ff541299(v=vs.85))。

当页面上发生特定类型的更改时，属性表会向对话框过程发送 [WM_NOTIFY](https://go.microsoft.com/fwlink/p/?linkid=181554) 消息。 对话框过程应准备好从消息参数中提取通知代码，并做出相应的响应。

有关对话框过程可能会遇到的通知的详细信息（例如 PSN_APPLY 或 PSN_HELP 通知）以及过程应如何处理它们，请参阅 Windows SDK 文档中的 [通知](https://go.microsoft.com/fwlink/p/?linkid=181555) 。

### <a name="psn_apply-notifications"></a><a href="" id="psn-apply-notifications"></a>PSN_APPLY 通知

当用户单击 **"确定**"、" **关闭**" 或 " **应用**" 时，属性表将发送 PSN_APPLY 通知消息。 在此消息中，对话框过程应该验证并应用用户所做的更改。

当收到 PSN_APPLY 通知时，提供程序必须执行以下操作：

1.  如果尚未执行此操作，请获取设备安装参数的指针， (设备 [**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a) 结构) 。 此结构可通过以下方式获得：调用[**SetupDiGetDeviceInstallParams**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinstallparamsa)，传递在 PROPSHEETPAGE 结构的**lParam**成员引用的区域中传递的已保存*DeviceInfoSet*和*DeviceInfoData* 。

2.  确保用户的更改有效。

3.  如果提供程序允许用户设置需要 Windows 删除和重新启动设备的属性，则提供程序必须在返回的 SP_DEVINSTALL_PARAMS 结构的 **FLAGSEX** 字段中设置 DI_FLAGSEX_PROPCHANGE_PENDING 标志。

    但是，如果提供程序可以确保更改不需要停止和重新启动设备的驱动程序，则无需设置此标志。

4.  与已更改的[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)结构一起调用[**SetupDiSetDeviceInstallParams**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdeviceinstallparamsa) ，以设置新参数。

### <a name="psn_reset-notifications"></a><a href="" id="psn-reset-notifications"></a>PSN_RESET 通知

当用户单击 " **取消**" 时，属性表将发送 PSN_RESET 通知消息。 对于此消息，对话框过程应丢弃用户所做的任何更改。

 

