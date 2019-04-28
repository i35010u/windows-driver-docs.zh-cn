---
title: 安全密钥注入
description: 安全密钥注入
ms.assetid: 21F8ED59-B04C-40D3-AEED-015890798215
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56843d10d3555f7b21f53785f7304f95e0eda6d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339120"
---
# <a name="secure-key-injection"></a>安全密钥注入


安全密钥注入加密传输的敏感材料从服务器应用程序到智能卡通过不受信任的客户端提供支持。 安全密钥注入正常工作，必须执行以下步骤：

1.  加密密钥的建立：

    1.  在服务器与客户端上的智能卡之间使用共享对称密钥。
    2.  生成临时对称会话密钥在服务器上的并导入到智能卡。 必须由具有生成智能卡上的相应私钥的公钥加密会话密钥。
    3.  从共享对称密钥派生会话密钥。 有关详细信息，请参阅[ **CardGetSharedKeyHandle**](https://msdn.microsoft.com/library/windows/hardware/dn468730)。
    4.  使用 DH 密钥派生。

2.  服务器上的数据加密：

    1.  数据可能是如 PIN 身份验证数据。
    2.  数据可能是如 RSA/ECC 的非对称密钥对。

3.  客户端上的智能卡中的数据解密。

下图显示了服务器应用程序会生成一个密钥，然后到客户端安全地将密钥传输跨信任边界。 收到该密钥后，客户端将其导入到智能卡。 作为最后一步，该密钥导入的 CA 存档。 服务器应用程序和智能卡之间应存在加密的通道，客户端应用程序/微型驱动程序应不能用于访问加密的数据。

![在使用智能卡安全密钥注入过程的服务器客户端交互的概述](images/seckeyinj.png)

若要加密在步骤 2 中的密钥，在服务器和智能卡需要共享的对称密钥。

为了适应在执行安全密钥注入时使用专用格式的现有卡，微型驱动程序可以加载在服务器端上不存在的卡。 微型驱动程序设置消息的格式，然后最后对其进行加密，它允许在对消息进行解密的客户端运行同一个微型驱动程序。

下图概述了服务器/客户端密钥存档与微型驱动程序。

![服务器/客户端密钥存档与微型驱动程序概述](images/seckeyarch.png)

## <a name="span-idcardkeyhandlespanspan-idcardkeyhandlespanspan-idcardkeyhandlespancard-key-handle"></a><span id="Card_Key_Handle"></span><span id="card_key_handle"></span><span id="CARD_KEY_HANDLE"></span>卡密钥句柄


使用对称密钥，卡处理时\_密钥\_句柄应该用于传递各地的密钥句柄。

``` syntax
typedef ULONG_PTR  CARD_KEY_HANDLE;
```

## <a name="span-idnocardmodespanspan-idnocardmodespanspan-idnocardmodespan-no-card-mode"></a><span id="_No_Card_Mode"></span><span id="_no_card_mode"></span><span id="_NO_CARD_MODE"></span> 无卡模式


为了便于格式化并使用同一个微型驱动程序安装在不受信任客户端上的加密数据的服务器应用程序[ **CardAcquireContext** ](https://msdn.microsoft.com/library/windows/hardware/dn468701)可以在不需要的模式下调用必须存在的卡。 设置以下标志可启用此模式下*dwFlags*的参数**CardAcquireContext** 。

``` syntax
#define CARD_SECURE_KEY_INJECTION_NO_CARD_MODE  0x1
```

此设置会指示[ **CardAcquireContext** ](https://msdn.microsoft.com/library/windows/hardware/dn468701)不需要任何卡读取器中。 这意味着，中的 ATR 字段[**卡\_数据**](https://msdn.microsoft.com/library/windows/hardware/dn468748)未被填充并**hSCard**并**hSCardCtx**设置为零。

当设置此标志时，微型驱动程序可以接受仅以下函数调用：

-   [**MDImportSessionKey**](https://msdn.microsoft.com/library/windows/hardware/dn468757)
-   [**MDEncryptData**](https://msdn.microsoft.com/library/windows/hardware/dn468756)
-   [**CardGetSharedKeyHandle**](https://msdn.microsoft.com/library/windows/hardware/dn468730)
-   [**CardGetAlgorithmProperty**](https://msdn.microsoft.com/library/windows/hardware/dn468722)
-   [**CardDestroyKey**](https://msdn.microsoft.com/library/windows/hardware/dn468720)
-   [**CardGetKeyProperty**](https://msdn.microsoft.com/library/windows/hardware/dn468728)
-   [**CardSetKeyProperty**](https://msdn.microsoft.com/library/windows/hardware/dn468739)
-   [**CardProcessEncryptedData**](https://msdn.microsoft.com/library/windows/hardware/dn468732)

## <a name="span-idusecasescenarioforsecurekeyinjectionspanspan-idusecasescenarioforsecurekeyinjectionspanspan-idusecasescenarioforsecurekeyinjectionspanuse-case-scenario-for-secure-key-injection"></a><span id="Use_Case_Scenario_for_Secure_Key_Injection"></span><span id="use_case_scenario_for_secure_key_injection"></span><span id="USE_CASE_SCENARIO_FOR_SECURE_KEY_INJECTION"></span>用例场景中的安全密钥注入


在此示例方案，客户端应用程序请求从智能卡所有者代表的服务器运行的 CA 应用程序将颁发的证书。 CA 还需要密钥存档。 请参阅部分中的脚注安全密钥注入有关使用非对称密钥对来建立临时对称会话密钥的指导。

用户密钥是在服务器端上生成、 存档和使用安全密钥注入函数注入到用户的智能卡。 下图说明了该过程。

![密钥生成和插入过程](images/skiusecase.png)

此方案基于导入使用非对称密钥进行加密的对称会话密钥，然后为后续密钥包装使用此对称密钥。

以下步骤介绍的过程中，如上图所示：

1.  客户端应用程序从服务器运行的 CA 应用程序请求新证书。
2.  当它收到客户端的请求时，服务器应用程序将检测已为密钥恢复配置的证书模板。 因此，服务器应用程序启动安全密钥注入协议。
3.  客户端应用程序调用[ **CardGetProperty** ](https://msdn.microsoft.com/library/windows/hardware/dn468729)为 CP\_密钥\_导入\_支持，以发现以下：

    -   是否在卡支持安全密钥注入。
    -   支持的对称密钥导入的方法。
    -   支持哪些算法。

4.  它通过非对称机制支持密钥注入到客户端应用程序指示微型驱动程序 (卡\_键\_导入\_非对称\_KEYEST)。
5.  客户端应用程序中查找智能卡以查看是否适用于密钥导入任何容器的容器映射文件。 如果找不到，客户端应用程序调用[ **CardCreateContainer** ](https://msdn.microsoft.com/library/windows/hardware/dn468708)以生成新密钥对。
6.  微型驱动程序指示智能卡来创建密钥对。
7.  创建密钥后，智能卡微型驱动程序到返回的键。
8.  微型驱动程序返回到客户端应用程序密钥在生成的指示。
9.  客户端应用程序现在调用[ **CardGetContainerInfo** ](https://msdn.microsoft.com/library/windows/hardware/dn468725)导出步骤 6 中创建的密钥对的公钥。
10. 卡微型驱动程序指示要返回的公钥的卡片。
11. 卡从卡中提取公钥 (K1)，并将其返回给微型驱动程序。
12. 微型驱动程序返回到客户端应用程序 K1。
13. 客户端应用程序调用[ **CardGetProperty** ](https://msdn.microsoft.com/library/windows/hardware/dn468729)枚举卡支持的对称算法，以及作为枚举可用于版 K1 的填充方案。
14. 微型驱动程序返回的算法和填充模式的支持。
15. 客户端应用程序将 K1 发送回服务器应用程序，以及描述的对称密钥算法和填充模式的卡支持的信息。
16. 通过使用卡支持的算法之一，服务器应用程序生成的对称密钥 (S1)。 对称密钥 S1 版 K1 使用加密，并返回到客户端应用程序。 服务器应用程序也会返回信息的加密算法和填充的类型被用来加密 S1。
17. 客户端应用程序调用[ **CardImportSessionKey** ](https://msdn.microsoft.com/library/windows/hardware/dn468731)到 K1 和任何填充信息以用于解密该 BLOB 的引用以及加密密钥数据 BLOB。

    关键数据 Blob 的详细信息的详细信息，请参阅[ **BCRYPT\_密钥\_数据\_BLOB\_标头**](https://msdn.microsoft.com/library/windows/desktop/aa375524)。

18. 微型驱动程序将加密的 BLOB 数据传递给智能卡进行解密。
19. 对称密钥进行解密后，智能卡微型驱动程序到返回对称密钥的引用。
20. 微型驱动程序返回对称密钥的客户端应用程序密钥句柄。
21. 客户端应用程序将确认发送到服务器应用程序已导入的对称密钥。
22. 服务器应用程序将导入 S1 到服务器端微型驱动程序通过调用[ **MDImportSessionKey**](https://msdn.microsoft.com/library/windows/hardware/dn468757)。
23. 服务器端微型驱动程序返回成功指示 S1 已成功导入。
24. 服务器应用程序生成的非对称密钥对 (K2)。 K2 发送到服务器端微型驱动程序通过调用[ **MDEncryptData**](https://msdn.microsoft.com/library/windows/hardware/dn468756)。 服务器应用程序生成 IV 和链接模式，并将该信息设置为服务器端微型驱动程序，通过调用[ **CardSetKeyProperty**](https://msdn.microsoft.com/library/windows/hardware/dn468739)。
25. 服务器端微型驱动程序通过使用 S1，加密 K2，并返回加密的 K2 的服务器应用程序。
26. 服务器应用程序将 encryptedK2 发送到客户端应用程序，以及与加密相关的任何信息。 这包括 IV 和链接模式信息。
27. 客户端应用程序调用[ **CardSetKeyProperty** ](https://msdn.microsoft.com/library/windows/hardware/dn468739)以指示哪些 IV 和链接的模式下使用 S1 微型驱动程序。 然后，客户端应用程序调用[ **CardProcessEncryptedData** ](https://msdn.microsoft.com/library/windows/hardware/dn468732)与以下数据：

    -   加密的密钥数据包含 K2 的 BLOB。
    -   以便卡可以对数据进行解密并创建项，则键引用到 S1。

28. 微型驱动程序执行必要的步骤来准备新的密钥容器，并提供智能卡加密的密钥数据 BLOB。
29. 智能卡对 K2 使用 S1 进行解密，并生成 K2 的新密钥容器。 卡返回成功指示已导入密钥。
30. 微型驱动程序返回成功从[ **CardProcessEncryptedData**](https://msdn.microsoft.com/library/windows/hardware/dn468732)。
31. 客户端应用程序返回成功，该过程已完成。

 

 





