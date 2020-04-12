---
title: NDIS/WIFI 验证
description: NDIS/WIFI 验证选项确定 NDIS 或 WIFI 驱动程序是否正确与 Windows 操作系统内核交互。
ms.assetid: EB553449-9460-403D-8ED2-343048C4B38C
ms.date: 04/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: b12907ab66033600c98bb34f1d55f711e3eeb28d
ms.sourcegitcommit: 84be9e06fd0886598df77dffcbc75632d613c8f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/11/2020
ms.locfileid: "81208132"
---
# <a name="ndiswifi-verification"></a>NDIS/WIFI 验证

NDIS/WIFI 验证选项确定 NDIS 或 WIFI 驱动程序是否正确与 Windows 操作系统内核交互。

**请注意**  此选项可从 Windows 8.1 开始使用。

NDIS/WIFI 验证选项应用规则，以验证您的驱动程序是否正确处理各种环境中的 Oid，并遵循 Microsoft 推荐的最佳做法。

如果此选项处于活动状态，并且驱动程序验证器检测到驱动程序违反了某个 NDIS 或 WIFI 规则，则驱动程序验证程序问题 bug 检查0xC4 （参数1等于特定符合性规则的标识符）。

验证规则列表包括以下各项：

[**NdisOidComplete**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoidcomplete)

[**NdisOidDoubleComplete**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoiddoublecomplete)

[**NdisOidDoubleRequest**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoiddoublerequest)

[**NdisTimedDataHang**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimeddatahang)

[**NdisTimedDataSend**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimeddatasend)

[**NdisTimedOidComplete**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimedoidcomplete)

[**WlanAssert**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlanassert)

[**WlanAssociation**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlanassociation)

[**WlanConnectionRoaming**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlanconnectionroaming)

[**WlanDisassociation**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlandisassociation)

[**WlanTimedAssociation**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedassociation)

[**WlanTimedConnectionRoaming**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedconnectionroaming)

[**WlanTimedConnectRequest**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedconnectrequest)

[**WlanTimedScan**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedscan)

[**WlanTimedLinkQuality**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedlinkquality)

## <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


你可以通过使用驱动程序验证器管理器或 Verifier 命令行来激活一个或多个驱动程序的 NDIS/WIFI 验证功能。 有关详细信息，请参阅[选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。 你必须重新启动计算机以激活或停用 NDIS/WIFI 验证选项。

-   **在命令行中**

    在命令行中，NDIS/WIFI 验证由**verifier/flags 0x200000** （第21位）表示。 若要激活 NDIS/WIFI 验证，请使用0x200000 的标志值或将0x200000 添加到标志值。 例如：

    ```
    verifier /flags 0x200000 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

-   **使用驱动程序验证器管理器**

    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入**Verifier** 。
    2.  选择 "**创建自定义设置（对于代码开发人员）** "，然后单击 "**下一步**"。
    3.  选择 "**从完整列表中选择单个设置**"。
    4.  选择（检查） **NDIS/WIFI 验证**。
    5.  重启计算机。

 

 





