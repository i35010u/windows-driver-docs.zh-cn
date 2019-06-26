---
title: NDIS/WIFI 验证
description: NDIS/WIFI 验证选项用于确定是否 NDIS 或 WIFI 驱动程序在与 Windows 操作系统内核正确交互。
ms.assetid: EB553449-9460-403D-8ED2-343048C4B38C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2591d071020b5859f49c57291d56c1d60fb9f470
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355067"
---
# <a name="ndiswifi-verification"></a>NDIS/WIFI 验证


NDIS/WIFI 验证选项用于确定是否 NDIS 或 WIFI 驱动程序在与 Windows 操作系统内核正确交互。

**请注意**  此选项是从 Windows 8.1 开始提供。

 

NDIS/WIFI 验证选项将应用规则，以验证您的驱动程序正确处理各种上下文中的 Oid 并遵循 Microsoft 建议的最佳实践。

如果此选项处于活动状态并且驱动程序验证程序检测到驱动程序违反了 NDIS 或 WIFI 规则之一，驱动程序验证程序 （与参数 1 等于特定符合性规则的标识符) 问题 bug 检查 0xC4。

验证规则的列表包括：

[**NdisOidComplete**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoidcomplete)

[**NdisOidDoubleComplete**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoiddoublecomplete)

[**NdisOidDoubleRequest**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoiddoublerequest)

[**NdisTimedDataHang**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimeddatahang)

[**NdisTimedDataSend**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimeddatasend)

[**NdisTimedOidComplete**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimedoidcomplete)

[**WlanAssociation**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlanassociation)

[**WlanConnectionRoaming**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlanconnectionroaming)

[**WlanDisassociation**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlandisassociation)

[**WlanTimedAssociation**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedassociation)

[**WlanTimedConnectionRoaming**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedconnectionroaming)

[**WlanTimedConnectRequest**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedconnectrequest)

[**WlanTimedScan**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedscan)

[**WlanTimedLinkQuality**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedlinkquality)

## <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的 NDIS/WIFI 验证功能。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。 必须重新启动计算机以激活或停用 NDIS/WIFI 验证选项。

-   **在命令行**

    在命令行中，NDIS/WIFI 验证为由**verifier /flags 0x200000** （位 21）。 若要激活 NDIS/WIFI 验证，使用 0x200000 标志值，或将 0x200000 添加到标志值。 例如：

    ```
    verifier /flags 0x200000 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

-   **使用驱动程序验证程序管理器**

    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择 （选中） **NDIS/WIFI 验证**。
    5.  重新启动计算机。

 

 





