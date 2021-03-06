---
title: MB SMS 操作
description: MB SMS 操作
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: 69e92188b7cb655017f1e3a51bf16af6b5d472e6
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248505"
---
# <a name="mb-sms-operations"></a>MB SMS 操作


本主题介绍使用短消息服务 (SMS) MB 设备的功能配置、读取/接收、发送和删除消息的操作。

SMS 支持是必需的。 小型端口驱动程序必须在 [**WWAN \_ 设备 \_ Cap**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps)结构的 **WwanSmsCaps** 成员中处理 [OID \_ WWAN \_ 设备 \_ cap](./oid-wwan-device-caps.md)查询请求时设置相应的发送和接收短信功能标志。 如果微型端口驱动程序不支持短信，它们应该指定 WWAN \_ sms \_ cap \_ NONE， \_ 并 \_ \_ \_ 为所有 SMS 相关 oid 返回 wwan 状态 "sms 未知错误"。

小型端口驱动程序只应在 [OID \_ WWAN \_ 就绪 \_ 信息](./oid-wwan-ready-info.md) 返回 **WwanReadyStateInitialize** 作为设备就绪状态后处理 SMS 操作。 仅当设备在提供程序网络上注册后，小型端口驱动程序才应处理某些 SMS 操作，如发送 SMS 消息 (但不一定) 的数据服务注册。

MB 服务不区分设备中提供的不同消息存储区。 因此，微型端口驱动程序必须处理所有消息存储，并使用虚拟索引访问单个虚拟消息存储区。 例如，如果设备有三个消息存储，则微型端口驱动程序必须整体处理所有这些消息，并将它们作为单个消息存储显示到服务中。

MB 驱动程序模型支持以下 SMS 操作：

-   SMS 配置

-   阅读短信

-   发送短信

-   删除短信

建议使用微型端口驱动程序来支持 SMS 配置、读取、发送和删除操作，以及向用户通知设备收到的任何新 SMS 消息。

有关 SMS 操作的详细信息，请 [参阅 \_ oid \_ wwan sms \_ 配置](./oid-wwan-sms-configuration.md)、 [oid \_ wwan \_ sms \_ 读取](./oid-wwan-sms-read.md)、 [oid \_ wwan \_ sms \_ 发送](./oid-wwan-sms-send.md)、 [oid \_ wwan \_ sms \_ 删除](./oid-wwan-sms-delete.md)和 [OID \_ wwan \_ sms \_ 状态](./oid-wwan-sms-status.md)。

### <a name="relevant-services-and-drivers"></a>相关的服务和驱动程序

*SmsRouterSvc.dll* -与 WwanSvc 交互以处理发送和接收图像的服务

WinRT SMS API *MbSmsApi.dll* 实现

*UT_SmsRouter.dll* -载入到实际的设备测试


## <a name="sms-architectureflows"></a>SMS 体系结构/流

### <a name="sms-block-diagram"></a>SMS 块示意图
![SMS 体系结构流](images/mb-sms-architecture.png)

### <a name="sms-app-registration"></a>SMS 应用注册
![SMS 应用注册](images/mb-sms-appregistration.png)

### <a name="send-sms"></a>发送短信
![SMS 发送消息](images/mb-sms-send.png)

### <a name="api-receive-message"></a>API 接收消息
![API 接收消息](images/mb-sms-apireceive.png)

### <a name="app-lifecycle"></a>应用生命周期
![SMS 应用生命周期](images/mb-sms-lifecycle.png)

### <a name="service-lifecycle"></a>服务生命周期
![服务生命周期](images/mb-sms-servicelifecycle.png)

## <a name="testing"></a>测试

### <a name="automated-sms-tests"></a>自动短信测试

以下测试将自动执行，并且载入到 RI-TP。 它们每天运行并应传递100%。

* MobilebroadbandExperience\SmsApi

* MobilebroadbandExperience\SMSCDMA

* MobilebroadbandExperience\SMSDecodingTests

* MobilebroadbandExperience\SMSEncodingTests

* WWAN\SMS\Service\UnitTests

*SmsApi* 测试具有在桌面和 onecoreuap 上运行的不同版本。 由于 SMS 的 CDMA 部分不会移植到 *vnelibrary.dll* (c # 版本) ，桌面仍然使用 *vnelib.dll* (c + + 版本) 。 因此，您会发现两个版本的功能测试列表。

## <a name="hardware-lab-kit-hlk-tests"></a>硬件实验室工具包 (HLK) 测试

这些是当前可用的与 MB-SMS 相关的 HLK 测试：

* TestSms
    - [CDMA](/windows-hardware/test/hlk/testref/d089c8f6-8973-4cd0-8931-cdc851dd1ee3)、 [GSM](/windows-hardware/test/hlk/testref/0045e280-e26a-44fe-88ec-98c6975a713b)

* TestSmsStoreFull
    - [CDMA](/windows-hardware/test/hlk/testref/fe377fdd-5fd6-40c4-a032-37f5d14a4c37)、 [GSM](/windows-hardware/test/hlk/testref/836c93b2-d6f4-4b23-b4af-d14d01547f08)

* TestWake
    - CDMA： [IncomingDataPacket](/windows-hardware/test/hlk/testref/eab2386a-1936-48d9-bdc2-3c89d5372fc5)、 [RegisterStateChange](/windows-hardware/test/hlk/testref/d10ef539-a40f-4496-8183-c4d57c7eaf40)
    - GSM： [IncomingDataPacket](/windows-hardware/test/hlk/testref/dab51ae1-91fc-4ce8-87e7-954a9128fce7)、 [RegisterStateChange](/windows-hardware/test/hlk/testref/0f3f0b8f-356c-4434-ab35-3208e6e1631f) 

* TestSimBad
    - [GSM](/windows-hardware/test/hlk/testref/2be175c8-69a0-45a8-ad8a-01efa2cb393c)

* TestDeviceCapsEx
    - [CDMA](/windows-hardware/test/hlk/testref/e4ec5199-0841-4864-ac17-b6b71f81cdf3)
    - [GSM](/windows-hardware/test/hlk/testref/75c812d5-8c7d-4589-8336-7d72f2feb987)

* TestSIMNotInserted
    - [GSM](/windows-hardware/test/hlk/testref/92b164f7-c0e6-4231-99e7-e51070c4bdf6)

### <a name="running-tests"></a>正在运行测试 

可以通过 netsh 运行测试列表和 HLK 测试。 有关使用 netsh 工具的详细信息，请参阅 [**netsh mbn**](/windows-server/networking/technologies/netsh/netsh-mbn)  and [**netsh mbn test 安装**](mb-netsh-mbn-test.md)。

```
netsh mbn test feature=sms testpath="C:\data\test\bin" taefpath="C:\data\test\bin" param="AccessString=internet"
```

可以使用以下说明收集和解码日志： [MB 收集日志](mb-collecting-logs.md)。

## <a name="special-messages"></a>特殊消息

### <a name="operator-messages"></a>操作员消息

操作员可以预配设备来处理特定消息。 此功能不再可用，但尚未完全删除该功能。 代码 ProvisioningEngine 处理操作员通知。 有关详细信息，请参阅 [操作员通知](/windows-hardware/drivers/mobilebroadband/enabling-mobile-operator-notifications-and-system-events) 和 [操作员事件](/windows-hardware/drivers/mobilebroadband/mobile-operator-notification-event-technical-details)。

### <a name="broadcast-messages"></a>广播消息

有关通过 SMS 的紧急警报的详细信息，请参阅 [SmsBroadcastMessage](/uwp/api/windows.devices.sms.smsbroadcastmessage) 和 [SmsBroadcastType](/uwp/api/windows.devices.sms.smsbroadcasttype)。


## <a name="uwp-capabilities-for-sms"></a>适用于 SMS 的 UWP 功能

### <a name="legacy-sms-api"></a>旧版 SMS API
有两个旧的 SMS Api： *sms* 和 *smsSend*。

### <a name="latest-sms-api"></a>最新 SMS API

* *cellularMessaging*

有关详细信息，请参阅 [UWP 短信](/uwp/api/Windows.Devices.Sms)。

## <a name="other-relevant-links"></a>其他相关链接

* [开发短信应用](/windows-hardware/drivers/mobilebroadband/developing-sms-apps)
