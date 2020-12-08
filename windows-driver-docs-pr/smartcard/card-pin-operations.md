---
title: 卡 PIN 操作
description: 卡 PIN 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 198521d0a685d590a560a34ea05e09d09f1831ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804931"
---
# <a name="card-pin-operations"></a>卡 PIN 操作


由于它在 ATM 计算机的数字键盘上首次使用，因此它从银行业继承而来。 其他一些行业文档使用 "卡持有人验证" (CHV) 。 了解到数据格式不只是数值，但也可以是用户可以提供的任何形式的任何内容。 作为 PIN 数据传递的值由互操作性注意事项约束为 ANSI 单字节字符集。

用户的身份验证与管理员身份验证的差别很大，因为用户通常不具有拥有管理身份验证机密的特权。 这对可以使用哪种类型的数据及其处理方式有很多影响。 如果在客户端计算机上使用管理机密来执行某些操作，例如，通过中心颁发机构提供帮助来取消阻止用户的卡，则必须将此数据安全地传输到此卡，否则不会泄露任何可能性，否则，它将不会在当前事务之外提供任何值。 将安全传输到卡的难点在于，不建议使用 PIN 对管理员进行身份验证。

身份验证仅在事务内有效，以防止其他应用程序劫持经过身份验证的会话。 Deauthentication 在结束事务时自动发生。

更改 PIN 必须使安全令牌失效。

## <a name="span-idgeneral_definitionsspanspan-idgeneral_definitionsspanspan-idgeneral_definitionsspangeneral-definitions"></a><span id="General_Definitions"></span><span id="general_definitions"></span><span id="GENERAL_DEFINITIONS"></span>常规定义


为插针定义了两种数据类型：一个用于描述与角色和 PIN 集相关联的单个 pin，这些 pin \_ 用于带有 pin 标识符的位掩码。 此外，我们还废止了用户名的字符串，并引入了转换为 PIN 标识符的角色号。 我们还定义了两个标志，用于 PIN 更改操作，此规范稍后将对此进行说明。

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

若要在功能上等效于当前卡微型驱动程序卡，则必须至少为所有卡片预配三个角色：角色 \_ EVERYONE、角色 \_ 用户和角色 \_ 管理员。 每个角色都等效于 \_ 卡片上的一个 PIN ID。 卡只有一个真正的管理员角色，但可以有多个角色可取消阻止其他角色。 但是，只有一个角色应控制访问权限以执行管理员级别的操作（如删除文件系统），这是角色 \_ 管理员。 此外，角色 \_ 管理员必须能够取消阻止角色 \_ 用户。 还有一个用户角色，该角色提供对卡的文件系统的访问权限。 其他角色3到7是可选的，只能与密钥容器关联。

有关可应用于只读卡的特殊注意事项，请参阅本规范后面的 "只读卡"。

## <a name="span-idsecret_typespanspan-idsecret_typespansecret_type"></a><span id="SECRET_TYPE"></span><span id="secret_type"></span>机密 \_ 类型


下面的枚举描述了 PIN 的类型。

```ManagedCPlusPlus
typedef enum
{
    AlphaNumericPinType = 0,    // Regular PIN
    ExternalPinType,            // External PIN
    ChallengeResponsePinType,   // Challenge/Response PIN
    EmptyPinType                // No PIN
} SECRET_TYPE;
```

**注意**  当遇到 PIN **机密 \_ TYPEEmptyPinType** 时，Windows 不会提示输入 pin，也不会调用 **CardAuthenticatePin** 或 **CardAuthenticatePinEx**。 如果需要无条件访问卡片上的材料，此设置很有用。



## <a name="span-idsecret_purposespanspan-idsecret_purposespansecret_purpose"></a><span id="SECRET_PURPOSE"></span><span id="secret_purpose"></span>机密 \_ 用途


**Pin \_ 信息** 数据结构使用以下枚举来描述用于用户信息用途的 pin 目的。

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

Windows 使用枚举值向用户显示一条描述当前请求的卡 PIN 的相应消息。 微型驱动程序完全控制 \_ 要使用的机密类型。 下面是包含示例上下文字符串的 "PIN 提示" 对话框的图例。

!["固定" 对话框](images/pinbox.png)

图中的第一个字符串 ( "Enter PIN。 注册： BaseRSASmartcardLogon ") 由调用应用程序提供，用于提供应用程序上下文。 如果不存在应用程序上下文字符串，则对话框将显示标准文本。

第二个字符串 ( "请输入您的身份验证 PIN" ) 由 **机密 \_ 用途** 通过以下方式之一驱动：

-   默认上下文字符串

    默认情况下，基本 CSP 显示以下预定义的字符串，这些字符串已进行了相应的本地化。

    | 字符串名称        |  String                                          |
    |---------------------|--------------------------------------------------|
    | AuthenticationPin   | "请输入身份验证 PIN。"          |
    | DigitalSignaturePin | "请输入数字签名 PIN。"       |
    | EncryptionPin       | "请输入你的加密 PIN。"              |
    | NonRepudiationPin   | "请输入您的不可否认性 PIN。"         |
    | AdministratorPin    | "请输入管理员 PIN。"           |
    | PrimaryCardPin      | "请输入你的 PIN 码"。                         |
    | UnblockOnlyPin      | "请输入你的 PIN 来解除阻止用户 PIN。" |



-   自定义字符串

    开发人员可以通过以下方式重写默认上下文字符串：在微型驱动程序的注册表项的注册表项中的注册表项中设置自定义字符串 (HKLM\ \\ software software \\ \\ Microsoft \\ 密码 \\ Calais \\ 智能 \\ 卡 xyz，其中 XYZ 是卡微型驱动程序) 的名称。

    若要重写预定义的上下文字符串，请使用自定义字符串将注册表字符串值添加到微型驱动程序的注册表项。 密钥名称用于设置要重写的 **机密 \_ 用途** 预定义上下文字符串，其中包含0x80000100，它对应于 **机密 \_ 类型** 和开头的第一个成员。 不能只重写一个字符串、部分或全部上下文字符串。

    字符串的值应遵循以下格式：

    ``` syntax
    “LangID,xxxx;LangID,xxxxx”
    ```

    **注意**  自定义字符串周围的引号不会得到正确处理，因此不应依赖于防止分析字符串中的特殊字符。




**注意**  为同一区域设置包含两个不同的自定义字符串将导致选取第一个自定义字符串。




对话框中的第三个字符串 ( "数字签名 PIN" ) 是一个预定义的字符串，由 **PIN \_ 信息** 数据结构中的 **机密 \_ 用途** 值决定。

对于 **UnblockOnlyPin**，预期用途是取消阻止用户 PIN。 此 PIN 不得用于任何其他目的。

## <a name="span-id_pin_cache_policy_typespanspan-id_pin_cache_policy_typespan-pin_cache_policy_type"></a><span id="_PIN_CACHE_POLICY_TYPE"></span><span id="_pin_cache_policy_type"></span> PIN \_ 缓存 \_ 策略 \_ 类型


下面的枚举描述要与此 PIN 关联的 PIN 缓存策略。

```ManagedCPlusPlus
typedef enum
{
    PinCacheNormal = 0,
    PinCacheTimed,
    PinCacheNone,
    PinCacheAlwaysPrompt
} PIN_CACHE_POLICY_TYPE;
```

下表描述了基本 CSP 如何处理三种不同的缓存模式。

| 缓存模式               | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **PinCacheNormal**       | 对于此模式，将根据每个登录 ID 的每个进程的基本 CSP 缓存 PIN。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **PinCacheTimed**        | 在此模式下，在指定的时间段内，在给定的时间段内，PIN 会无效， (值以秒为单位) 。 这是通过在将 PIN 添加到缓存时记录时间戳来实现的，然后验证此时间戳与访问 PIN 的时间。 这意味着 PIN 可能在缓存中的时间长于指定的时间戳，但在过期后不会使用。 在内存中加密 PIN 以使其受到保护。                                                                                                                |
| **PinCacheNone**         | 当无法缓存 PIN 时，基本 CSP 绝不会将 PIN 添加到缓存中。 当使用 [**CryptSetProvParam**](/windows/win32/api/wincrypt/nf-wincrypt-cryptsetprovparam) 调用基本 CSP/KSP 来设置 pin 时，会将 pin 提交到卡进行验证，但不会进行缓存。 这意味着，任何后续操作都必须在基本 CSP 事务超时过期之前发生。                                                                                                                                                                                                                  |
| **PinCacheAlwaysPrompt** | 与 **PinCacheNone** 不同，设置此缓存模式时，基本 CSP 事务超时不适用。 将从用户收集 PIN，然后在每次需要身份验证的调用之前提交到卡进行验证。 调用 [**CryptSetProvParam**](/windows/win32/api/wincrypt/nf-wincrypt-cryptsetprovparam) 和 [**NCRYPTSETPROPERTY**](/windows/win32/api/ncrypt/nf-ncrypt-ncryptsetproperty) 以设置 pin 返回错误 SUCCESS， \_ 而不验证和缓存 pin。 这意味着，如果调用需要身份验证，则使用无提示上下文的应用程序的调用将失败。 |



**注意**  如果未缓存 PIN，Windows 登录可能无法正常工作。 此行为是设计使然。 因此，在将 PIN 缓存模式设置为 **PinCacheNormal** 以外的任何值时，应仔细考虑。



## <a name="span-id_pin_cache_policyspanspan-id_pin_cache_policyspan-pin_cache_policy"></a><span id="_PIN_CACHE_POLICY"></span><span id="_pin_cache_policy"></span> PIN \_ 缓存 \_ 策略


PIN 缓存策略结构包含描述 PIN 缓存策略的信息。 除了介绍与此 PIN 缓存策略关联的信息外，还介绍了 PIN 缓存类型。 此关联信息的一个示例是在策略指示 **PinCacheTimed** 时 PIN 缓存的超时值。

```ManagedCPlusPlus
#define      PIN_CACHE_POLICY_CURRENT_VERSION   6

typedef struct _PIN_CACHE_POLICY
{
    DWORD                   dwVersion;
    PIN_CACHE_POLICY_TYPE   PinCachePolicyType;
    DWORD                   dwPinCachePolicyInfo;
} PIN_CACHE_POLICY, *PPIN_CACHE_POLICY;
```

## <a name="span-idpin_infospanspan-idpin_infospanpin_info"></a><span id="PIN_INFO"></span><span id="pin_info"></span>PIN \_ 信息


PIN 对象结构包含描述 PIN 的信息。 其中介绍了 PIN 类型、允许解除阻止此目标 PIN 的 pin 以及 PIN 缓存策略。 在基本 CSP/KSP 获取 PIN 信息结构后，应在数据缓存中缓存数据文件的缓存方式。

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

**DwUnblockPermission** 成员是一个位掩码，用于说明哪些 pin 有权取消阻止 PIN。 权限基于指定 Pin 的按位 "or"。 对于取消阻止操作，卡微型驱动程序应忽略任何自引用。 角色 \_ 用户将拥有 "0x00000100" 的 "更新" 权限位掩码。 这意味着角色管理员可以取消对其的阻止 \_ 。 角色 \_ 管理员，其更新权限为0x00000000。 这意味着不能解除阻止。

**DwFlags** 成员包含 PIN 标志。 目前仅定义了一个标志： PIN \_ 信息 \_ 需要 \_ 安全 \_ 输入。 此标志指示基本 CSP/KSP 是否需要安全桌面来输入 PIN 码。

**注意**  使用此结构可以为 \_ 每个人授予更改或取消阻止 PIN 的权限。 我们不建议这样做，并且不会在微型驱动程序 API 中提供任何机制，以允许角色 \_ 更改或取消阻止 PIN。
