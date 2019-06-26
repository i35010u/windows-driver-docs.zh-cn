---
title: 网络驱动程序的安全问题
description: 本部分介绍特定于网络驱动程序的安全问题
ms.assetid: 04400213-9bd4-4dbe-b302-24917450829f
keywords:
- 网络驱动程序 WDK，安全性
- 安全 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 414046a7bd47f40a35ad726bc05dbd13ef2373c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382118"
---
# <a name="security-issues-for-network-drivers"></a>网络驱动程序的安全问题

有关编写安全的驱动程序的常规讨论，请参阅[创建可靠的内核模式驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)。

以下安全的编码实践和常规设备驱动程序指南，超出网络驱动程序应执行以下操作来增强安全性：

- 所有网络驱动程序应都验证从注册表中读取的值。 具体而言的调用方[ **NdisReadConfiguration** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreadconfiguration)或[ **NdisReadNetworkAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreadnetworkaddress)必须不进行任何假设有关值从注册表中读取和必须验证它会读取每个注册表值。 如果调用方**NdisReadConfiguration**确定超出界限是一个值，它应改为使用默认值。 如果调用方**NdisReadNetworkAddress**确定一个值是超出界限，则应改为使用永久介质访问控制 (MAC) 地址或默认地址。

## <a name="oid-specific-issues"></a>特定于 OID 的问题

- 微型端口驱动程序，请在其[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)或[ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)函数，应验证任何对象标识符请求的驱动程序的 (OID) 值设置。 如果该驱动程序确定要设置的值超出界限，则应失败集请求。 有关对象标识符的详细信息，请参阅[获取和设置微型端口驱动程序的信息和 NDIS 支持 WMI](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)。

- 如果中间驱动程序的*MiniportOidRequest*函数不会将设置操作中传递给基础的微型端口驱动程序，该函数应验证 OID 值。 有关详细信息，请参阅[中间驱动程序查询和设置操作](intermediate-driver-query-and-set-operations.md)。

### <a name="query-oid-security-guidelines"></a>查询 OID 安全指导原则

大多数查询 Oid 可以由系统上的任何用户模式应用程序颁发。 对于查询 Oid 遵循这些特定的准则。

1. 始终验证缓冲区的大小过大的输出。 而不输出缓冲区大小检查任何查询 OID 处理程序是安全性错误。

    ```c++
    if (oid->DATA.QUERY_INFORMATION.InformationBufferLength < sizeof(ULONG)) {
        oid->DATA.QUERY_INFORMATION.BytesNeeded = sizeof(ULONG);
        return NDIS_STATUS_INVALID_LENGTH;
    }
    ```

2. 始终写入 BytesWritten 正确和最小值。 它是一个红色标志，若要将分配`oid->BytesWritten = oid->InformationBufferLength`类似下面的示例执行的操作。

    ```c++
    // ALWAYS WRONG
    oid->DATA.QUERY_INFORMATION.BytesWritten = DATA.QUERY_INFORMATION.InformationBufferLength; 
    ```

    操作系统将返回到用户模式应用程序复制 BytesWritten 字节。 如果 BytesWritten 为大于实际编写了驱动程序，字节数，则操作系统可能最终会将复制回到未初始化的内核内存到用户模式，则会出现信息泄漏漏洞。 相反，使用类似于以下代码：

    ```c++
    oid->DATA.QUERY_INFORMATION.BytesWritten = sizeof(ULONG);
    ``` 

3. 永远不会返回从缓冲区读取的值。 在某些情况下，输出缓冲区的 oid 是直接映射到的恶意用户模式进程。 已写入后，恶意的过程可以更改输出缓冲区。 例如，下面的代码可能会遭到攻击，因为攻击者可以更改 NumElements 写入该值后：

    ```c++
    output->NumElements = 4;
    for (i = 0 ; i < output->NumElements ; i++) {
        output->Element[i] = . . .;
    }
    ```
    若要避免读取返回的缓冲区，保留本地副本。 例如，若要解决上面的示例中，引入新的堆栈变量：

    ```c++
    ULONG num = 4;
    output->NumElements = num;
    for (i = 0 ; i < num; i++) {
        output->Element[i] = . . .;
    }
    ```

    使用此方法时，返回的驱动程序的堆栈变量显示为循环`num`而不是从其输出缓冲区。 该驱动程序还应将标记与输出缓冲区`volatile`关键字来阻止编译器以无提示方式撤消此修补程序。

### <a name="set-oid-security-guidelines"></a>设置 OID 安全指导原则

可以通过运行中的管理员或系统安全组的用户模式应用程序颁发大多数设置的 Oid。 尽管它们是通常受信任的应用程序，微型端口驱动程序仍必须允许使用的内存损坏或内核代码注入。 为设置 Oid 遵循以下特定的规则：

1.  始终验证输入有足够空间。 而无需输入的缓冲区大小检查任何 OID 组处理程序中存在安全漏洞。

    ```c++
    if (oid->DATA.SET_INFORMATION.InformationBufferLength < sizeof(ULONG)) {
        return NDIS_STATUS_INVALID_LENGTH;
    }
    ```

2. 只要验证与嵌入的偏移量 OID，则必须验证嵌入的缓冲区是在 OID 负载。 这需要多个检查。 例如， [OID_PM_ADD_WOL_PATTERN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern)交付的嵌入的模式，需要检查。 纠正验证需要检查：

    1. InformationBufferSize > = sizeof(NDIS_PM_PACKET_PATTERN)

        ```c++
        PmPattern = (PNDIS_PM_PACKET_PATTERN) InformationBuffer;
        if (InformationBufferLength < sizeof(NDIS_PM_PACKET_PATTERN))
        {
            Status = NDIS_STATUS_BUFFER_TOO_SHORT;
            *BytesNeeded = sizeof(NDIS_PM_PACKET_PATTERN);
            break;
        }
        ```

    2. 模式-> PatternOffset + 模式-> PatternSize 都不会溢出

        ```c++
        ULONG TotalSize = 0;
        if (!NT_SUCCESS(RtlUlongAdd(Pattern->PatternOffset, Pattern->PatternSize, &TotalSize) ||
            TotalSize > InformationBufferLength) 
        {
            return NDIS_STATUS_INVALID_LENGTH;
        }
        ```

        可以使用如下例所示的代码组合这些两个检查：

        ```c++
        ULONG TotalSize = 0;
        if (InformationBufferLength < sizeof(NDIS_PM_PACKET_PATTERN) ||
            !NT_SUCCESS(RtlUlongAdd(Pattern->PatternSize, Pattern->PatternOffset, &TotalSize) ||
            TotalSize > InformationBufferLength) 
        {
            return NDIS_STATUS_INVALID_LENGTH;
        }
        ```
   
    3. InformationBuffer + 模式-> PatternOffset + 模式-> PatternLength 都不会溢出

        ```c++
        ULONG TotalSize = 0;
        if (!NT_SUCCESS(RtlUlongAdd(Pattern->PatternOffset, Pattern->PatternLength, &TotalSize) ||
            (!NT_SUCCESS(RtlUlongAdd(TotalSize, InformationBuffer, &TotalSize) ||
            TotalSize > InformationBufferLength) 
        {
            return NDIS_STATUS_INVALID_LENGTH;
        }
        ```

    4. 模式-> PatternOffset + 模式-> PatternLength < = InformationBufferSize

        ```c++
        ULONG TotalSize = 0;
        if(!NT_SUCCESS(RtlUlongAdd(Pattern->PatternOffset, Pattern->PatternLength, &TotalSize) ||
            TotalSize > InformationBufferLength)) 
        {
            return NDIS_STATUS_INVALID_LENGTH;
        }
        ```
   
### <a name="method-oid-security-guidelines"></a>方法 OID 安全指导原则

可以通过运行中的管理员或系统安全组的用户模式应用程序颁发方法 Oid。 它们是指南的一组和一个查询的组合，因此这两个前面的列也适用于方法 Oid。

## <a name="other-network-driver-security-issues"></a>其他网络驱动程序安全问题

- 许多 NDIS 微型端口驱动程序通过使用 NdisRegisterDeviceEx 公开控制设备。 执行此操作的那些必须审核它们 IOCTL 的处理程序，使用作为 WDM 驱动程序的所有相同的安全规则。 有关详细信息，请参阅[I/O 控制代码的安全问题](https://docs.microsoft.com/windows-hardware/drivers/kernel/security-issues-for-i-o-control-codes)。

- 设计良好的 NDIS 微型端口驱动程序不应依赖于在特定进程上下文中，调用和紧密的合作与用户模式 （与 Ioctl 和 Oid 正在异常） 进行交互。 它将是一个红色标志，以查看微型端口已打开 usermode 句柄、 执行 usermode 等待或分配内存中的 usermode 配额。 该代码应进行调查。

- 大多数 NDIS 微型端口驱动程序应该不会涉及到分析数据包有效负载。 在某些情况下，不过，它可能有必要。 因此，应非常仔细地审核此代码，如果作为驱动程序解析来自不受信任源的数据。

- 由于分配内核模式内存时，则是标准，NDIS 驱动程序应使用适当[NX 池选择的机制](https://docs.microsoft.com/windows-hardware/drivers/kernel/nx-pool-opt-in-mechanisms)。 在 WDK 8 和更高版本，则`NdisAllocate*`系列函数都正确选择。

