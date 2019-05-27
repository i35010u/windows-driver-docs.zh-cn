---
title: 在 Windows 上的移动运营商和 Oem 的 esim 卡管理
description: 在 Windows 上的移动运营商和 Oem 的 esim 卡管理
ms.assetid: 7D37D297-76FD-46DA-ACC3-73E4BF970524
ms.date: 05/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 82f14e695ad7973f560110f025a95e40d29038bb
ms.sourcegitcommit: 6152f92c5d2bc7c8db08dd0fdbc0146f88e8413b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2019
ms.locfileid: "66224506"
---
# <a name="esim-management-on-windows-for-mobile-operators-and-oems"></a>在 Windows 上的移动运营商和 Oem 的 esim 卡管理

## <a name="mobile-operators-and-oems"></a>移动运营商和 Oem

如果是移动运营商或 OEM 并且想要在 Windows 上支持 esim 卡管理，请按照下列步骤：

1. 进行硬件 Lab Kit (HLK) 测试运行。 这可确保 Windows 10 esim 卡支持的调制解调器硬件兼容性。 Oem 和 Odm 必须确保以下 HLK esim 卡测试执行：
    1. 基本 esim 卡支持测试用例：
        - [Win6_4.MB.CDMA.Data.TestLowLevelUiccAccess](https://docs.microsoft.com/windows-hardware/test/hlk/testref/f27c8d81-7e2b-49d1-be4c-614bf62f003c)
        - [Win6_4.MB.GSM.Data.TestLowLevelUiccAccess](https://docs.microsoft.com/en-us/windows-hardware/test/hlk/testref/104db926-5cc4-47ad-a7d0-ff476b0f57a1)
    2. 适用于 Windows 10 设备使用可移动的 SIM 槽和焊料的 eUICC:
        - [Win6_4.MB。CDMA。Data.TestSlot](https://docs.microsoft.com/windows-hardware/test/hlk/testref/049a0532-3d58-49aa-ac3d-2a9b8aab24a7)和/或[Win6_4.MB。GSM。Data.TestSlot](https://docs.microsoft.com/windows-hardware/test/hlk/testref/defddebe-cc40-4d6f-9b0c-ca5ca9a1cb4d)
        - [Win6_4.MB。CDMA。Data.TestDeviceCapsEx](https://docs.microsoft.com/windows-hardware/test/hlk/testref/e4ec5199-0841-4864-ac17-b6b71f81cdf3)和/或[Win6_4.MB。GSM。Data.TestDeviceCapsEx](https://docs.microsoft.com/windows-hardware/test/hlk/testref/75c812d5-8c7d-4589-8336-7d72f2feb987)

Windows 提供了移动设备管理提供程序来管理企业用例中的 esim 卡配置文件的功能。 但是，Windows 不限制生态系统合作伙伴可能想要向其自己的合作伙伴和/或客户提供这的方式。 在这种情况下，可以通过集成与 Windows 的 OMA-DM 支持 esim 卡配置文件的管理功能。 这样，可以远程管理根据公司策略的 esim 卡配置文件。

如果你想要集成和使用只有一个 MDM 提供程序，请直接联系该提供程序。 如果你想要提供给客户使用不同 MDM 提供程序，请联系 esim 卡管理[业务流程协调程序提供程序](https://www.idemia.com/esim-management-facilitation)。 业务流程协调程序提供程序充当处理 MDM 载入，以及移动运营商载入代理。 他们[角色](https://www.idemia.com/smart-connect-hub)是为所有参与方作为轻松，而且可缩放，尽可能使该过程。

## <a name="esim-management-for-other-audiences"></a>针对其他受众的 esim 卡管理

如果您是 MDM 提供程序，并想要在 Windows 上支持 esim 卡管理，请参阅[如何移动设备管理提供程序支持在 Windows 上的 esim 卡管理](https://docs.microsoft.com/windows/client-management/mdm/esim-enterprise-management)。

如果您是最终用户在组织中，并且想要 esim 卡用于你的组织提供的设备上的移动电话网络数据连接，请参阅[esim 卡用于获取 Windows 10 电脑上的移动电话网络数据连接](https://support.microsoft.com/help/4020763/windows-10-use-esim-for-cellular-data)。