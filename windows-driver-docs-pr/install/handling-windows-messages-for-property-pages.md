---
title: 处理 Windows 消息的属性页
description: 处理 Windows 消息的属性页
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
ms.openlocfilehash: c7648e76a22ea1e88b9eb28caa73b0173d5e692c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523327"
---
# <a name="handling-windows-messages-for-property-pages"></a>处理 Windows 消息的属性页





当[设备属性页提供程序](types-of-device-property-page-providers.md)请求来创建其设备或设备类的属性页的句柄，它将返回为属性页对话框过程的地址。 对话框过程必须进行初始化的属性页时收到 WM_INITDIALOG 消息时，必须准备好时获取 WM_NOTIFY 消息处理对设备属性的更改。 该过程还可以处理任何其他此类消息可能需要，Microsoft Windows SDK 文档中所述。

WM_INITDIALOG 消息响应，对话框过程初始化的属性页中的信息。 此类信息可能包括表示设备、 设备和其即插即用设备描述的友好名称的图标。

[**SetupDiLoadClassIcon** ](https://msdn.microsoft.com/library/windows/hardware/ff552053)加载指定的设备类的图标，并返回的句柄可以对后续调用中使用的加载大图标**SendDlgItemMessage**。 例如：

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

ClassIcon 中返回的句柄可以转换为 SendDlgItemMessage 函数所需的 WPARAM 中。 在示例中，IDC_TEST_ICON 标识接收 STM_SETICON 消息的对话框中的控件。 必须提供程序中定义的 IDC_TEST_ICON 值。 有关操作图标和位图的其他函数，请参阅[设备安装函数](https://msdn.microsoft.com/library/windows/hardware/ff541299)。 有关详细信息**SendDlgItemMessage**， **DestroyIcon**，并在对话框中使用的图标，请参阅 Windows SDK 文档。

表示设备的图标，除了典型的设备属性页包括说明或"友好名称"的设备，并且显示了设备属性的当前设置。 插即用 (PnP) 管理器存储在注册表中的每个设备的即插即用属性。 属性页提供程序可以调用[ **SetupDiGetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551967)若要获取此类属性的值。 如果特定于设备或类配置信息已也存储在注册表中作为安装过程的一部分，属性页提供程序可以使用其他**SetupDiXxx**函数来提取显示该信息。 有关详细信息，请参阅[设备安装函数](https://msdn.microsoft.com/library/windows/hardware/ff541299)。

属性表页上发生某些类型的更改，当发送[WM_NOTIFY](https://go.microsoft.com/fwlink/p/?linkid=181554)对话框过程的消息。 对话框过程应准备好从消息参数中提取通知代码并做出相应的响应。

有关对话框过程可能会遇到的通知，如 PSN_APPLY 或 PSN_HELP 通知和过程应如何处理它们的详细信息，请参阅[通知](https://go.microsoft.com/fwlink/p/?linkid=181555)Windows SDK 中文档。

### <a href="" id="psn-apply-notifications"></a>PSN_APPLY 通知

属性表发送 PSN_APPLY 通知消息，当用户单击**确定**，**关闭**，或**应用**。 此消息的响应，对话框过程应验证和应用的用户所做的更改。

当它收到 PSN_APPLY 通知时，该提供程序必须执行以下步骤：

1.  如果它具有这样做，获得到的设备安装参数的指针 ([**SP_DEVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552346)结构) 的设备。 此结构是可通过调用[ **SetupDiGetDeviceInstallParams**](https://msdn.microsoft.com/library/windows/hardware/ff551104)，并传递保存*DeviceInfoSet*和*DeviceInfoData*引用的区域中传递**lParam** PROPSHEETPAGE 结构中的成员。

2.  确保用户的更改有效。

3.  如果访问接口允许用户将需要删除并重新启动设备的 Windows 属性设置，该提供程序必须设置 DI_FLAGSEX_PROPCHANGE_PENDING 标志**FlagsEx**返回 SP_DEVINSTALL_PARAMS 字段结构。

    但是，如果提供程序可以确保所做的更改不需要的设备驱动程序已停止并重新启动，它不会不需要设置此标志。

4.  调用[ **SetupDiSetDeviceInstallParams** ](https://msdn.microsoft.com/library/windows/hardware/ff552141)使用已更改[ **SP_DEVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552346)结构，以设置新的参数。

### <a href="" id="psn-reset-notifications"></a>PSN_RESET 通知

属性表发送 PSN_RESET 通知消息，当用户单击**取消**。 此消息的响应，对话框过程应丢弃用户所做的任何更改。

 

 





