---
title: 安全密钥注入
description: 安全密钥注入
ms.assetid: 21F8ED59-B04C-40D3-AEED-015890798215
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc9130dab72d159070435decb258a453ed940979
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423844"
---
# <a name="secure-key-injection"></a>安全密钥注入


安全密钥注入支持从服务器应用程序到智能卡的加密传输从服务器应用程序到智能卡。 要使安全密钥注入正常工作，必须执行以下步骤：

1.  加密密钥的建立：

    1.  在服务器与客户端上的智能卡之间使用共享对称密钥。
    2.  在服务器上生成临时对称会话密钥并将其导入到智能卡。 必须通过在智能卡上生成相应私钥的公钥来加密会话密钥。
    3.  从共享对称密钥派生会话密钥。 有关详细信息，请参阅 [**CardGetSharedKeyHandle**](/previous-versions/dn468730(v=vs.85))。
    4.  使用 DH 密钥派生。

2.  服务器上的数据加密：

    1.  数据可以是身份验证数据，如 PIN。
    2.  数据可以是非对称密钥对，如 RSA/ECC。

3.  客户端智能卡上的数据解密。

下图显示了一个服务器应用程序，该应用程序生成密钥，然后将密钥安全地传输到客户端的信任边界。 接收到密钥后，客户端会将其导入智能卡。 作为最后一步，将密钥导入到 CA 以进行存档。 服务器应用程序与智能卡之间应该存在一个加密通道，并且客户端应用程序/微型驱动程序应该无法访问加密的数据。

![服务器-在使用智能卡注入安全密钥时的客户端交互概述](images/seckeyinj.png)

若要对步骤2中的密钥进行加密，服务器和智能卡需要共享对称密钥。

若要在执行安全密钥注入时容纳使用专用格式的现有卡，可以在服务器端加载微型驱动程序，而无需使用该卡。 微型驱动程序设置消息的格式，最后对消息进行加密，这允许在客户端上运行的同一个微型驱动程序对消息进行解密。

下图提供了使用微型驱动程序进行服务器/客户端密钥存档的概述。

![微型驱动程序的服务器/客户端密钥存档概述](images/seckeyarch.png)

## <a name="span-idcard_key_handlespanspan-idcard_key_handlespanspan-idcard_key_handlespancard-key-handle"></a><span id="Card_Key_Handle"></span><span id="card_key_handle"></span><span id="CARD_KEY_HANDLE"></span>卡键句柄


处理对称密钥时， \_ \_ 应使用卡键句柄来传递密钥句柄。

``` syntax
typedef ULONG_PTR  CARD_KEY_HANDLE;
```

## <a name="span-id_no_card_modespanspan-id_no_card_modespanspan-id_no_card_modespan-no-card-mode"></a><span id="_No_Card_Mode"></span><span id="_no_card_mode"></span><span id="_NO_CARD_MODE"></span> 无卡模式


为了使服务器应用程序可以使用安装在不受信任的客户端上的相同微型驱动程序来格式化和加密数据，可以在不需要使用卡的模式下调用 [**CardAcquireContext**](/previous-versions/dn468701(v=vs.85)) 。 通过在**CardAcquireContext**的*dwFlags*参数中设置以下标志来启用此模式。

``` syntax
#define CARD_SECURE_KEY_INJECTION_NO_CARD_MODE  0x1
```

此设置指示 [**CardAcquireContext**](/previous-versions/dn468701(v=vs.85)) 不会将任何卡片置于读取器中。 这意味着 [**卡 \_ 数据**](/previous-versions/dn468748(v=vs.85)) 中的 ATR 字段未填充，并且 **hSCard** 和 **hSCardCtx** 设置为零。

设置此标志后，微型驱动程序只能接受以下函数调用：

-   [**MDImportSessionKey**](/previous-versions/dn468757(v=vs.85))
-   [**MDEncryptData**](/previous-versions/dn468756(v=vs.85))
-   [**CardGetSharedKeyHandle**](/previous-versions/dn468730(v=vs.85))
-   [**CardGetAlgorithmProperty**](/previous-versions/dn468722(v=vs.85))
-   [**CardDestroyKey**](/previous-versions/dn468720(v=vs.85))
-   [**CardGetKeyProperty**](/previous-versions/dn468728(v=vs.85))
-   [**CardSetKeyProperty**](/previous-versions/dn468739(v=vs.85))
-   [**CardProcessEncryptedData**](/previous-versions/dn468732(v=vs.85))

## <a name="span-iduse_case_scenario_for_secure_key_injectionspanspan-iduse_case_scenario_for_secure_key_injectionspanspan-iduse_case_scenario_for_secure_key_injectionspanuse-case-scenario-for-secure-key-injection"></a><span id="Use_Case_Scenario_for_Secure_Key_Injection"></span><span id="use_case_scenario_for_secure_key_injection"></span><span id="USE_CASE_SCENARIO_FOR_SECURE_KEY_INJECTION"></span>安全密钥注入的用例方案


在此示例方案中，客户端应用程序请求颁发证书的 CA 应用程序是代表智能卡所有者在服务器上运行的。 CA 还要求密钥存档。 有关使用非对称密钥的指导原则建立临时的对称会话密钥，请参阅安全密钥注入部分的脚注。

用户密钥是在服务器端生成的，并使用安全密钥注入函数在用户的智能卡上进行存档并注入。 下图说明了该过程。

![密钥生成和插入的过程](images/skiusecase.png)

此方案基于导入使用非对称密钥加密的对称会话密钥，然后使用此对称密钥进行后续的密钥包装。

以下步骤描述了上图中所示的过程：

1.  客户端应用程序从服务器上运行的 CA 应用程序请求新的证书。
2.  接收客户端的请求时，服务器应用程序会检测到已为密钥恢复配置了证书模板。 因此，服务器应用程序会启动安全密钥注入协议。
3.  客户端应用程序[**CardGetProperty**](/previous-versions/dn468729(v=vs.85))为 CP \_ 密钥 \_ 导入支持调用 CardGetProperty \_ ，以发现以下内容：

    -   卡是否支持安全密钥注入。
    -   支持哪种对称密钥导入方法。
    -   支持的算法。

4.  微型驱动程序向客户端应用程序指示它支持通过非对称机制进行密钥注入 (卡 \_ 密钥 \_ 导入 \_ 非对称 \_ KEYEST) 。
5.  客户端应用程序查看智能卡的容器映射文件，以查看是否有任何容器适用于密钥导入。 如果未找到任何内容，则客户端应用程序会调用 [**CardCreateContainer**](/previous-versions/dn468708(v=vs.85)) 来生成新的密钥对。
6.  微型驱动程序指示智能卡创建密钥对。
7.  创建密钥后，智能卡会将密钥返回到微型驱动程序。
8.  微型驱动程序会向客户端应用程序返回已生成密钥的指示。
9.  客户端应用程序现在调用 [**CardGetContainerInfo**](/previous-versions/dn468725(v=vs.85)) 来导出在步骤6中创建的密钥对的公钥。
10. 卡微型驱动程序指示卡返回公共密钥。
11. 该卡将从卡提取 (版 k1) 的公钥，并将其返回给微型驱动程序。
12. 微型驱动程序将版 k1 返回到客户端应用程序。
13. 客户端应用程序调用 [**CardGetProperty**](/previous-versions/dn468729(v=vs.85)) 来枚举卡支持的对称算法，并枚举可用于版 k1 的填充方案。
14. 微型驱动程序返回受支持的算法和填充模式。
15. 客户端应用程序会将版 k1 发送回服务器应用程序，并提供描述了卡支持的对称密钥算法和填充模式的信息。
16. 通过使用卡支持的算法之一，服务器应用程序 (S1) 生成对称密钥。 对称密钥 S1 通过版 k1 进行加密并返回到客户端应用程序。 服务器应用程序还会返回有关加密算法和用于加密 S1 的填充类型的信息。
17. 客户端应用程序使用加密密钥数据 BLOB 以及对版 k1 的引用以及用于解密 BLOB 的任何空白信息调用 [**CardImportSessionKey**](/previous-versions/dn468731(v=vs.85)) 。

    有关密钥数据 Blob 的详细信息，请参阅 [**BCRYPT \_ key \_ data \_ BLOB \_ HEADER**](/windows/win32/api/bcrypt/ns-bcrypt-bcrypt_key_data_blob_header)。

18. 微型驱动程序将加密的 BLOB 数据传递到智能卡进行解密。
19. 解密对称密钥后，智能卡会将对对称密钥的引用返回到微型驱动程序。
20. 微型驱动程序为对称密钥的客户端应用程序返回一个密钥句柄。
21. 客户端应用程序向服务器应用程序发送对对称密钥已导入的确认。
22. 服务器应用程序通过调用 [**MDImportSessionKey**](/previous-versions/dn468757(v=vs.85))将 S1 导入服务器端微型驱动程序。
23. 服务器端微型驱动程序返回 success 以指示已成功导入 S1。
24. 服务器应用程序 (K2) 生成非对称密钥对。 通过调用 [**MDEncryptData**](/previous-versions/dn468756(v=vs.85))将 K2 发送到服务器端微型驱动程序。 服务器应用程序将生成 IV 和链式模式，并通过调用 [**CardSetKeyProperty**](/previous-versions/dn468739(v=vs.85))将此信息设置为服务器端微型驱动程序。
25. 服务器端微型驱动程序使用 S1 对 K2 进行加密，并将加密的 K2 返回给服务器应用程序。
26. 服务器应用程序会将 encryptedK2 发送到客户端应用程序，以及与加密有关的任何信息。 这包括 IV 和链接模式信息。
27. 客户端应用程序调用 [**CardSetKeyProperty**](/previous-versions/dn468739(v=vs.85)) ，以指示微型驱动程序与 S1 一起使用的 IV 和链接模式。 然后，客户端应用程序调用具有以下数据的 [**CardProcessEncryptedData**](/previous-versions/dn468732(v=vs.85)) ：

    -   包含 K2 的加密密钥数据 BLOB。
    -   对 S1 的键引用，以便卡可以解密数据并创建密钥。

28. 微型驱动程序执行必要的步骤来准备新的密钥容器，并向智能卡提供加密的密钥数据 BLOB。
29. 智能卡使用 S1 解密 K2，并为 K2 生成新的密钥容器。 该卡返回 success 以指示已导入密钥。
30. 微型驱动程序从 [**CardProcessEncryptedData**](/previous-versions/dn468732(v=vs.85))返回 success。
31. 客户端应用程序返回成功并完成该过程。

 

