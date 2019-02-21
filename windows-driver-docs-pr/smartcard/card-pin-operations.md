---
title: 卡 PIN 操作
description: 卡 PIN 操作
ms.assetid: 7993D284-8122-4831-9C00-E53DAEB7965F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9b74f5946c8f27e830f9230f0239ea27bad29fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522923"
---
# <a name="card-pin-operations"></a>卡 PIN 操作


PIN 已继承银行业由于 ATM 机数字键盘上其首次使用的术语。 一些其他行业文档使用术语卡持有者验证 (CHV)。 理解数据格式不是只是数值，但可以是任何内容，用户可以提供给表示出他或她可供使用。 如 PIN 数据受为 ANSI 单字节字符集的互操作性注意事项传递的值。

用户的身份验证与极大地从管理员的身份验证的用户通常不有权拥有管理身份验证密钥。 什么类型的数据可用于此和它的方式进行处理，这有许多含义。 如果客户端计算机上使用管理密钥来完成诸如取消用户卡阻止并借助于中央集权机构，此数据必须是安全地传输到而无需发生泄露的可能性，否则是完全临时以使其不具有当前事务外的任何值。 建议不要使用 PIN 才能进行身份验证管理员正是排列安全地传输到卡的难度。

身份验证是只在一个事务，以防止者劫持身份验证的会话的另一个应用程序中有效。 Deauthentication 时结束事务会自动发生。

更改 PIN 必须使安全令牌失效。

## <a name="span-idgeneraldefinitionsspanspan-idgeneraldefinitionsspanspan-idgeneraldefinitionsspangeneral-definitions"></a><span id="General_Definitions"></span><span id="general_definitions"></span><span id="GENERAL_DEFINITIONS"></span>常规定义


两种数据类型定义的 Pin： 一个用于描述与角色相关联的各个 Pin 和 PIN\_用于一个 PIN 标识符的位掩码的集。 此外，我们停止使用具有用户名称的字符串，并引入角色将转换为 PIN 标识符的数字。 我们还更高版本中此规范定义 PIN 更改操作的介绍了两个的标志。

```ManagedCPlusPlus
typedef     DWORD                      PIN_ID, *PPIN_ID;
typedef     DWORD                      PIN_SET, *PPIN_SET;

#define     MAX_PINS                   8

#define     ROLE_EVERYONE              0
#define     ROLE_USER                  1
#define     ROLE_ADMIN                 2

#define     PIN_SET_ALL_ROLES          0xFF
#define     CREATE_PIN_SET(PinId)      (1 << PinId)
#define     SET_PIN(PinSet, PinId)     PinSet |= CREATE_PIN_SET(PinId)
#define     IS_PIN_SET(PinSet, PinId)  (0 != (PinSet & CREATE_PIN_SET(PinId)))
#define     CLEAR_PIN(PinSet, PinId)   PinSet &= ~CREATE_PIN_SET(PinId)

#define     PIN_CHANGE_FLAG_UNBLOCK    0x01
#define     PIN_CHANGE_FLAG_CHANGEPIN  0x02
```

若要在功能上等效于当前卡微型驱动程序卡，必须使用至少三个角色设置所有卡：角色\_EVERYONE 角色\_用户和角色\_管理员。 每个角色相当于一个 PIN\_在卡上的 ID。 卡片，只有一个，则返回 true 的管理员角色，但可以有多个可取消阻止其他角色的角色。 但是，只有一个角色应控制访问，以执行管理员级操作，例如删除文件系统中，并且这是角色\_管理员。 此外，角色\_管理员必须能够取消阻止角色\_用户。 此外，还有只有一个用户角色提供访问权限的文件系统，一个卡。 其他角色 3 至 7 是可选的可以是仅与密钥容器相关联。

有关可以应用的特殊注意事项仅卡，请参阅"只读卡"更高版本中此规范。

## <a name="span-idsecrettypespanspan-idsecrettypespansecrettype"></a><span id="SECRET_TYPE"></span><span id="secret_type"></span>机密\_类型


以下枚举中描述的 PIN 的类型。

```ManagedCPlusPlus
typedef enum
{
    AlphaNumericPinType = 0,    // Regular PIN
    ExternalPinType,            // External PIN
    ChallengeResponsePinType,   // Challenge/Response PIN
    EmptyPinType                // No PIN
} SECRET_TYPE;
```

**请注意**时遇到 PIN**机密\_TYPEEmptyPinType**，Windows 不会提示输入 PIN，也不会调用**CardAuthenticatePin**或**CardAuthenticatePinEx**。 需要对在卡上的材料的无条件访问权限时，此设置很有用。



## <a name="span-idsecretpurposespanspan-idsecretpurposespansecretpurpose"></a><span id="SECRET_PURPOSE"></span><span id="secret_purpose"></span>机密\_用途


使用以下枚举**PIN\_信息**数据结构来描述用户信息用途的 PIN 的用途。

```ManagedCPlusPlus
typedef enum
{
    AuthenticationPin,      // Authentication PIN
    DigitalSignaturePin,    // Digital Signature PIN
    EncryptionPin,          // Encryption PIN
    NonRepudiationPin,      // Non Repudiation PIN
    AdministratorPin,       // Administrator PIN
    PrimaryCardPin,
    UnblockOnlyPin          // Unblocking other PINs
} SECRET_PURPOSE;
```

Windows 使用枚举值描述当前请求 PIN 的卡的用户显示相应的消息。 微型驱动程序完全控制哪些机密\_要使用的类型。 下面是举例说明了 PIN 提示对话框，其中包含示例上下文字符串。

![pin 对话框](images/pinbox.png)

第一个字符串在图中 ("输入 PIN。 注册：由调用应用程序提供应用程序上下文提供 BaseRSASmartcardLogon")。 如果没有应用程序的上下文字符串存在，则对话框将显示标准的文本。

第二个字符串 （"请输入你的身份验证 PIN"） 由驱动**机密\_用途**中通过以下方式之一：

-   默认上下文字符串

    默认情况下，基本 CSP 显示以下适当本地化的预定义的字符串。

    |                     |                                                  |
    |---------------------|--------------------------------------------------|
    | AuthenticationPin   | "请输入你的身份验证的 PIN。"          |
    | DigitalSignaturePin | "请输入你的数字签名的 PIN。"       |
    | EncryptionPin       | "请输入你的加密的 PIN。"              |
    | NonRepudiationPin   | "请输入你的 PIN 不可否认。"         |
    | AdministratorPin    | "请输入你的管理员 PIN"。           |
    | PrimaryCardPin      | "请输入您的 PIN。"                         |
    | UnblockOnlyPin      | "请输入你的 PIN 以解除锁定用户 PIN。" |



-   自定义字符串

    开发人员可以通过在以下注册表值的微型驱动程序的注册表项设置自定义字符串重写默认上下文字符串 (HKLM\\软件\\软件\\Microsoft\\加密\\Calais\\智能卡\\XYZ，其中 x y Z 是卡微型驱动程序的名称)。

    若要重写预定义的上下文字符串，请添加到自定义字符串的微型驱动程序的注册表项的注册表字符串值。 密钥的名称设置哪些**机密\_用途**预定义的上下文字符串被覆盖时，使用对应的第一个成员的 0x80000100**机密\_类型**和开始。 不能重写只是一个字符串，部分或全部上下文字符串。

    字符串的值应遵循以下格式：

    ``` syntax
    “LangID,xxxx;LangID,xxxxx”
    ```

    **请注意**自定义字符串周围的引号不正确处理和应不依赖于以防止分析该字符串中的特殊字符。




**请注意**包括两个不同的自定义字符串中第一个自定义字符串是相同的区域设置结果选取。




对话框 （"数字签名固定"） 中的第三个字符串是一个预定义的字符串，由**机密\_用途**中的值**PIN\_信息**数据结构。

有关**UnblockOnlyPin**，预期的目的是要解除阻止用户 PIN。 此 PIN 必须不能用于任何其他用途。

## <a name="span-idpincachepolicytypespanspan-idpincachepolicytypespan-pincachepolicytype"></a><span id="_PIN_CACHE_POLICY_TYPE"></span><span id="_pin_cache_policy_type"></span> PIN\_缓存\_策略\_类型


以下枚举说明缓存策略将与此 PIN 的 PIN。

```ManagedCPlusPlus
typedef enum
{
    PinCacheNormal = 0,
    PinCacheTimed,
    PinCacheNone,
    PinCacheAlwaysPrompt
} PIN_CACHE_POLICY_TYPE;
```

下表描述了基本 CSP 在三种不同的缓存模式时的处理方式。

| 缓存模式               | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **PinCacheNormal**       | 对于此模式下，PIN 缓存的基本 CSP 每个进程，每个登录 id。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **PinCacheTimed**        | 对于此模式，PIN 失效后指定期间内的时间 （指定值以秒为单位）。 这是通过 PIN 添加到缓存时进行记录时间戳，然后验证访问 PIN 时的时间与此时间戳进行实施。 这意味着 PIN 可能会在缓存中的时间比指定时间戳，但它已过期后将不会使用。 PIN 以使其受保护的内存中进行加密。                                                                                                                |
| **PinCacheNone**         | 不能缓存 PIN，基本 CSP 永远不会将 PIN 添加到缓存。 当使用称为基本 CSP/KSP [ **CryptSetProvParam** ](https://msdn.microsoft.com/library/windows/desktop/aa380276)设置 PIN，PIN 是提交到验证卡但不是会缓存。 这意味着任何后续操作必须出现之前基本 CSP 事务超时时间已到。                                                                                                                                                                                                                  |
| **PinCacheAlwaysPrompt** | 与不同**PinCacheNone**，当设置了此缓存模式，则不适合使用基本 CSP 事务超时时间。 从用户收集并提交到要求身份验证每次调用之前验证卡 PIN。 调用[ **CryptSetProvParam** ](https://msdn.microsoft.com/library/windows/desktop/aa380276)并[ **NcryptSetProperty** ](https://msdn.microsoft.com/library/windows/desktop/aa376292)设置 PIN 返回错误\_不成功正在验证和缓存 PIN。 这意味着，如果调用需要身份验证，从使用无提示的上下文的应用程序的调用将失败。 |



**请注意**如果未缓存 PIN，Windows 登录可能无法正常工作。 此行为是设计使然。 因此，应设置 PIN 缓存模式而不为任何值时提供仔细考虑**PinCacheNormal**。



## <a name="span-idpincachepolicyspanspan-idpincachepolicyspan-pincachepolicy"></a><span id="_PIN_CACHE_POLICY"></span><span id="_pin_cache_policy"></span> PIN\_缓存\_策略


PIN 缓存策略结构包含描述 PIN 缓存策略的信息。 它介绍了 PIN 缓存类型，除了与此 PIN 缓存策略的相关信息。 此关联信息的一个示例是 PIN 缓存的超时值时在策略指示**PinCacheTimed**。

```ManagedCPlusPlus
#define      PIN_CACHE_POLICY_CURRENT_VERSION   6

typedef struct _PIN_CACHE_POLICY
{
    DWORD                   dwVersion;
    PIN_CACHE_POLICY_TYPE   PinCachePolicyType;
    DWORD                   dwPinCachePolicyInfo;
} PIN_CACHE_POLICY, *PPIN_CACHE_POLICY;
```

## <a name="span-idpininfospanspan-idpininfospanpininfo"></a><span id="PIN_INFO"></span><span id="pin_info"></span>PIN\_信息


PIN 对象结构包含描述 PIN 信息。 它介绍了 PIN 允许取消阻止此目标的 PIN，以及缓存策略 PIN 的 PIN 类型。 获取由基本 CSP/KSP PIN 信息结构后，它应类似于数据文件的缓存方式的数据缓存中缓存它。

```ManagedCPlusPlus
#define      PIN_INFO_REQUIRE_SECURE_ENTRY       1

typedef struct _PIN_INFO
{
    DWORD                   dwVersion;
    SECRET_TYPE             PinType;
    SECRET_PURPOSE          PinPurpose;
    PIN_SET                 dwChangePermission;
    PIN_SET                 dwUnblockPermission;
    PIN_CACHE_POLICY        PinCachePolicy;
    DWORD                   dwFlags;
} PIN_INFO, *PPIN_INFO;
```

**DwUnblockPermission**成员是描述的 Pin 的位掩码已解除锁定 PIN 的权限。 权限基于指定的 Pin 上的按位或。 对于取消阻止操作，卡微型驱动程序应忽略任何自引用。 角色\_用户可以使用的 0x00000100 更新权限位掩码。 这意味着可以阻塞角色\_管理员。 角色\_管理员，具有 0x00000000 更新权限。 这意味着它不能是未被阻止。

**DwFlags**成员包含 PIN 标志。 目前，只有一个标志被定义:PIN\_INFO\_REQUIRE\_SECURE\_条目。 此标志指示到基本 CSP/KSP 安全桌面是否需要输入 PIN。

**请注意**就可以通过使用此结构来向角色授予\_EVERYONE 权限以更改或取消阻止一个 PIN。 我们不建议此操作，并且没有机制提供的微型驱动程序 API 以允许角色\_EVERYONE 以更改或取消阻止一个 PIN。











