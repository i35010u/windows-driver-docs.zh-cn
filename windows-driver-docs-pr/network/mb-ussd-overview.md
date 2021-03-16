---
title: USSD 概述
description: USSD 实现和测试
keywords: USSD，非结构化补充服务数据
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: 9b488e70ca790d532d24dceae76dcc02e804bd37
ms.sourcegitcommit: d624c81fe4bf92fc3d674c2f0bd99e58f6cf5e8a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2021
ms.locfileid: "103572160"
---
# <a name="ussd-overview"></a>USSD 概述

非结构化补充服务数据 (USSD) 是全球系统用于移动通信的通信协议 (GSM) 设备与移动网络操作员通信， (通常称为 "MO" ) 。

若要了解 USSD，请将其与最密切相关的同级：短消息服务 (SMS) 进行比较。 USSD 和 SMS 都是 GSM 标准，这意味着它们被引入为第二代移动设备中的功能。 不过，USSD 是基于会话的连接。 虽然 SMS 用于短会话的短信消息，但 USSD 通常用于移动设备的命令和控制。 由于需要维护会话，USSD 不支持将存储和转发功能作为 SMS。 USSD 和 SMS 消息都与与7位 GSM 兼容的字符一起发送，但 USSD 以至于耗光 out 184 个字符，而与160的短信。

可以通过打开拨号程序并键入代码，从手机发送 USSD 消息。 并非所有代码都受每个电话或 MO 的支持。 在某些情况下，电话软件或操作系统可能会阻止手动发送代码。 必须实现的一个必需代码为 * #06 #。 此代码将返回 (IMEI) 的国际移动设备标识符，但某些手机会阻止你直接拨打。 如果你通过手机的设置执行传统的方法来查找调制解调器的 IMEI，则使用此代码检索该数字。

如果电话硬件可以直接处理类似于 IMEI 示例中的代码命令，则不会启动网络会话。 其他需要网络通信的代码将打开一个会话，然后发送一条消息，其中包含一个命令和所有必要的参数（如果适用）。 这是一个用于检查当前余额和计划状态与 MO 的代码的示例。 

Windows 中的 USSD 实现为 WinRT API 图面。 此接口的实现类充当 USSD 会话的状态机，但最终依赖于 WWAN 服务来执行繁重的工作。 这些 Api 是使用工厂模式实现的。


## <a name="implementing-ussd"></a>实现 USSD
需要注意的一点是，由 IDL 定义的公共 API。 由于此原因，实现可能会造成混淆，尤其是在不熟悉 WinRT 的情况下。 其中的部分混乱来自 "工厂" 一词表面上不明确的用法。 工厂既可以引用静态接口的类实现，也可以引用为运行时类提供可激活接口的真实工厂。

本主题介绍了 WinRT 概念，然后基于这些概念介绍了实现。 为了进一步澄清，你可能始终引用 IDL。

界面

接口定义 (ABI) 的应用程序二进制接口。 它们描述了可对实现接口的任何类调用的函数。

运行时类

这些是实际的类。 它们按名称表示，最终作为类名称公开给 ABI。 每个运行时类可能具有零个或多个接口 (但如果有一个或多个接口) 、零个或多个静态接口，并在必要时必须声明至少一个默认接口。 这些接口中的每个接口都在不同的 "Impl" 类的不同文件中实现，它们似乎是单一的统一类到 ABI。

典型接口在现有对象上显示为实例方法。

静态接口作为运行时类本身的静态方法出现在客户端上。

可激活标记定义将生成运行时类的实例的工厂接口。 这会被完全模糊处理到客户端，并显示为该运行时类的构造函数。

### <a name="ussd-implementation"></a>USSD 实现

![显示 USSD 实现的关系图](images/ussd_implement.png?raw=true "implement_ussd_img")

## <a name="flow-open-send-receive-close"></a>Flow： Open、Send、Receive、Close。
### <a name="open-send"></a>打开，发送
![包含答复的 USSD 请求的流程图](images/ussd_request_with_reply.png?raw=true "resume_ussd_img")
1) 客户端使用其中一个静态函数 UssdSession CreateFromNetworkAccountId 或 UssdSession 来创建 UssdSession 对象。
2) 无论调用哪种 API，都需要使用网络接口 ID 初始化 UssdSession。 对于 * NetworkAccountID，将采取步骤从帐户 ID 检索网络接口 ID。
调用 CreateInternal () 来创建 UssdSession 的实例，并对新创建的实例调用 Initialize () 。 在初始化步骤中，将启动一个工作线程，并为该线程创建触发事件的事件句柄。 步骤3和4还会在实例的 Initialize () 期间发生。
3) 在 WwanWrapper 成员对象上调用 Initialize () 。 此函数接受静态回调函数以及上下文，以允许静态函数将回调映射到对象上下文。
4) WwanWrapper 通过提供静态回调函数指针并将 "this" 作为上下文来打开 WwanService、枚举接口并订阅 USSD 通知的句柄。
5) UssdSession 对象将返回到客户端。
6) 客户端通过使用消息字符串调用构造函数来构造新的 UssdMessage。 在此过程中，WinRT 进行模糊处理 UssdMessageFactory。
7) 客户端对会话对象调用 SendMessageAndGetReplyAsync，并传递 UssdMessage 实例。
8) 此时，SendMessageAndGetReplyAsync 创建一个名为 UssdSendMessageAndGetReplyOperation 的特殊操作对象。 从其名称开始，该对象将封装向下发送的单个消息的逻辑 (并等待回复) ，但这种情况并非如此。 WinRT 要求异步操作使用特殊的 out 参数，可将此参数视为此函数的定义上的第二个参数。 
    ```
    HRESULT SendMessageAndGetReplyAsync(
                [in] UssdMessage* message,
                [out, retval] Windows.Foundation.IAsyncOperation<UssdReply>** asyncInfo);
    ```
    它是 IUssdSendMessageAndGetReplyOperation，它是一个通过 typedef 的命名接口，通过此操作可避免返回 UssdReply，从而满足此参数。 此接口未在 IDL 中定义，但由 UssdSendMessageAndGetReplyOperationImpl 类实现。 请注意，此类的标头具有特殊扩展名：
    ```
    class UssdSendMessageAndGetReplyOperationImpl :
        public Microsoft::WRL::RuntimeClass<
            Windows::Networking::NetworkOperators::IUssdSendMessageAndGetReplyOperation,
            Windows::Internal::AsyncBaseFTM<IUssdSendMessageAndGetReplyCompletedHandler, Microsoft::WRL::SingleResult>>
    ```
    通过 UssdSendMessageAndGetReplyOperation 对象，WinRT 可以模糊处理此异步操作的复杂性以及与该操作一起提供的所有区室化和内存代理。 有关详细信息，请参阅 [SendMessageAndGetReplyAsync](/uwp/api/windows.networking.networkoperators.ussdsession.sendmessageandgetreplyasync)。

    现在，请了解上面所述的异步操作只是回调到 UssdSession 对象，其中实际包含了此操作的逻辑。 为了简单起见，UssdSession 本身会在此处封装工作。 现在，我们可以断言这一点，尽管有异步特性，一次只能发送一个 UssdMessage。
    
    SendMessageAndGetReplyAsync 函数的实际作用：

    * UssdSession 对象将更改为忙状态，存储 UssdMessage 的内容，并激发异步操作。
    * OnOperationStart () 是异步逻辑的入口点。 假设在此方案中没有活动会话。 此函数创建具有 RequestType = WwanUssdRequestInitiate 的 WWAN_USSD_REQUEST 对象。
    * 步骤9和步骤10作为此函数执行的操作发生。
        
9) m_wwanWrapper 调用 SendRequest 来处理将消息传递到 WwanService 的工作。
10) WwanWrapper 使用 WwanService 句柄调用 WwanService Api 来执行该操作。
        
### <a name="receive"></a>接收
![USSD 接收的流程图](images/ussd_resume.png?raw=true "resume_ussd_img")

在步骤10之后，我们将处于向 WwanService 发送请求以初始化新的 USSD 会话并在该会话下发送 USSD 消息的状态。 经过一段时间后，回复将可用。

11) WwanService 将通过还附加的上下文调用步骤4中提供的静态回调函数。
12) 上下文将用于检索 WwanWrapper 实例并调用 NotificationCallback () 。
13) WwanWrapper 将遵循与步骤11相同的模式，调用对 UssdSession 的静态回调，同时提供步骤3中存储的上下文。
14) 与步骤12类似，上下文用于对 UssdSession 的实例调用回调。
15) UssdSession 将 WWAN_USSD_EVENT (存储在锁定) 下，并通知工作线程处理事件。
16) HandleOperationReply () 使用现有的 UssdSendMessageAndGetReplyOperationImpl 对象，并将事件数据传递给其内部处理程序。
17) 该操作将构造并 UssdReply 并调用 FireCompletion () 将异步操作标记为 "已完成"。
18) WinRT 将异步操作的完成进行模糊处理到客户端。  (它们已等待操作或具有回调逻辑。 ) 

可以在同一会话下发送更多消息。 如果已维护会话，则将来的 RequestType 将为 WwanUssdRequestContinue。

### <a name="close"></a>关闭
![USSD 关闭的流程图](images/ussd_resume2.png?raw=true "resume_ussd_img") 步骤18之后，客户端收到了其 UssdMessage 的回复。 它们可能会也可能不会继续使用 active UssdSession 来发送其他消息。 我们假设在未来的某个时间点，客户端将在 UssdSession 上手动调用 Close () 。 如果客户端未显式调用 Close () ，它将在 UssdSession 的析构函数中调用。

19) 客户端调用 UssdSession 实例上的 Close () 。
20) 使用 RequestType = WwanUssdRequestCancel 创建 WWAN_USSD_REQUEST。
21) 请求将发送到 m_wwanWrapper，如步骤9中所示。
22) 请求发送到 WwanService，如步骤10所示。

此请求的结果并不重要。 对于所有意图和用途，会话将关闭。 即使在极端的情况下，如果消息从未送达，新的 USSD 会话也将始终覆盖现有的会话。


## <a name="hardware-lab-kit-hlk-tests"></a>硬件实验室工具包 (HLK) 测试
请参阅 [安装 HLK 的步骤](https://microsoft.sharepoint.com/teams/HWKits/SitePages/HWLabKit/Manual%20Controller%20Installation.aspx)。 

在 HLK Studio 中，连接到设备移动电话调制解调器驱动程序并运行测试： [Win6_4. MB。GSM.TestUssd](/windows-hardware/test/hlk/testref/17ae6fea-6244-442d-b977-6367d1ae441e)。

## <a name="mb-ussd-troubleshooting-guide"></a>MB USSD 故障排除指南
- 使用 [收集日志](mb-collecting-logs.md)中的说明收集和 decod 日志。

- 用于筛选的关键字
  1. OID_WWAN_USSD 
  1. NDIS_STATUS_WWAN_USSD
  1. WWAN_USSD_REQUEST
  1. WWAN_USSD_EVENT

## <a name="see-also"></a>另请参阅
[MB USSD 操作](mb-ussd-operations.md)

